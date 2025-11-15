# LunarOS Installation Guide

## Prerequisites

### Required Software

1. **LCC Compiler** (version 4.2 or later)
   - Download from: https://sites.google.com/site/lccretargetablecompiler/
   - Ensure `lcc` is in your PATH

2. **Build Tools**
   - GNU Make 3.8+ or compatible
   - NASM assembler (for x86 builds)
   - binutils (ld, ar, objcopy)

3. **Optional Tools**
   - QEMU (for testing)
   - VirtualBox or VMware (for VM deployment)
   - Git (for source code management)

## Installation Methods

### Method 1: Building from Source

#### Step 1: Download Source Code

```bash
# Via Git
git clone https://github.com/lunaros/lunaros.git
cd lunaros

# Or download release tarball
wget https://lunaros.org/releases/lunaros-1.0.tar.gz
tar xzf lunaros-1.0.tar.gz
cd lunaros-1.0
```

#### Step 2: Configure Build

```bash
# For x86 architecture
./configure --arch=x86 --compiler=lcc

# For ARM architecture
./configure --arch=arm --compiler=lcc

# Custom installation prefix
./configure --prefix=/opt/lunaros --arch=x86
```

Configuration options:
- `--arch=ARCH` - Target architecture (x86, arm)
- `--compiler=CC` - Compiler to use (lcc, gcc)
- `--prefix=DIR` - Installation directory
- `--debug` - Enable debug symbols
- `--enable-tests` - Build test suite

#### Step 3: Compile

```bash
# Build kernel and userspace
make all

# Parallel build for faster compilation
make -j4 all

# Build only kernel
make kernel

# Build only userspace
make userspace
```

#### Step 4: Create Bootable Image

```bash
# Create ISO image
make iso

# Create floppy image
make floppy

# Create hard disk image
make hdd
```

#### Step 5: Install (Optional)

```bash
# Install to system (requires root)
sudo make install

# Install to custom location
make install PREFIX=/custom/path
```

### Method 2: Pre-built Images

Download pre-built images from https://lunaros.org/downloads/

Available formats:
- `lunaros-x86.iso` - Bootable CD/DVD image
- `lunaros-x86-usb.img` - USB drive image
- `lunaros-x86-hdd.img` - Virtual hard disk image

## Deployment Options

### Option 1: Physical Hardware

#### USB Installation

**Linux/macOS:**
```bash
# Identify USB device
lsblk  # or: diskutil list (macOS)

# Write image (replace /dev/sdX with your device)
sudo dd if=lunaros-x86-usb.img of=/dev/sdX bs=4M status=progress
sudo sync
```

**Windows:**
1. Download Rufus: https://rufus.ie/
2. Select lunaros ISO/IMG file
3. Select target USB drive
4. Click "Start"

#### CD/DVD Installation

Burn `lunaros-x86.iso` to CD/DVD using:
- **Linux**: `brasero` or `k3b`
- **macOS**: Disk Utility
- **Windows**: ImgBurn or Windows built-in burner

### Option 2: Virtual Machine

#### QEMU

```bash
# Basic boot
qemu-system-i386 -cdrom lunaros.iso -m 128M

# With more features
qemu-system-i386 \
  -cdrom lunaros.iso \
  -m 256M \
  -enable-kvm \
  -net nic -net user \
  -soundhw ac97

# Boot from hard disk image
qemu-system-i386 -hda lunaros-hdd.img -m 256M
```

#### VirtualBox

```bash
# Create VM
VBoxManage createvm --name "LunarOS" --ostype "Linux_64" --register

# Configure VM
VBoxManage modifyvm "LunarOS" --memory 256 --vram 16 --cpus 1

# Create storage controller
VBoxManage storagectl "LunarOS" --name "IDE" --add ide

# Attach ISO
VBoxManage storageattach "LunarOS" \
  --storagectl "IDE" \
  --port 0 --device 0 \
  --type dvddrive \
  --medium lunaros.iso

# Start VM
VBoxManage startvm "LunarOS"
```

#### VMware

1. Create new virtual machine
2. Select "Other Linux 3.x kernel 64-bit"
3. Allocate 256 MB RAM minimum
4. Attach ISO to CD/DVD drive
5. Boot VM

### Option 3: Docker Container (Development)

```dockerfile
# Dockerfile for LunarOS development
FROM ubuntu:20.04

RUN apt-get update && apt-get install -y \
    build-essential \
    nasm \
    qemu-system-x86 \
    wget

# Install LCC
RUN wget https://sites.google.com/.../lcc-4.2.tar.gz && \
    tar xzf lcc-4.2.tar.gz && \
    cd lcc-4.2 && make && make install

WORKDIR /lunaros
COPY . .

RUN make all

CMD ["qemu-system-i386", "-cdrom", "lunaros.iso", "-m", "128M"]
```

```bash
# Build and run
docker build -t lunaros-dev .
docker run -it lunaros-dev
```

## Post-Installation

### First Boot

1. LunarOS will boot to a login prompt
2. Default credentials:
   - Username: `root`
   - Password: `lunaros`

3. Change root password immediately:
   ```bash
   passwd
   ```

### Initial Configuration

```bash
# Set hostname
echo "myhostname" > /etc/hostname

# Configure network (if supported)
ifconfig eth0 192.168.1.100 netmask 255.255.255.0
route add default gw 192.168.1.1

# Set timezone
ln -sf /usr/share/zoneinfo/America/New_York /etc/localtime
```

### Installing Development Tools

```bash
# LCC should be pre-installed, verify:
lcc -v

# Install additional tools from source
cd /usr/src
tar xzf make-3.82.tar.gz
cd make-3.82
./configure --prefix=/usr
make
make install
```

## Troubleshooting

### Build Issues

**Problem**: `lcc: command not found`
```bash
# Solution: Install LCC and add to PATH
export PATH=/usr/local/lcc/bin:$PATH
```

**Problem**: `make: *** No rule to make target 'kernel'`
```bash
# Solution: Run configure first
./configure --arch=x86 --compiler=lcc
```

**Problem**: Assembly errors during build
```bash
# Solution: Install NASM
# Ubuntu/Debian: sudo apt-get install nasm
# macOS: brew install nasm
```

### Boot Issues

**Problem**: VM doesn't boot
- Verify BIOS boot order (CD/DVD first)
- Check ISO integrity: `md5sum lunaros.iso`
- Try different VM software

**Problem**: Kernel panic on boot
- Increase RAM allocation (minimum 64 MB)
- Check hardware virtualization support
- Try safe mode boot option

**Problem**: No display output
- Ensure VGA-compatible graphics
- Try different display resolution settings
- Check VM display settings

### Installation Issues

**Problem**: USB drive not bootable
- Verify image was written correctly
- Check USB drive is not write-protected
- Try different USB port or drive

**Problem**: Cannot mount filesystem
- Check disk space
- Verify filesystem support in kernel
- Try reformatting target drive

## Verification

### Verify Installation

```bash
# Check kernel version
uname -a

# Check LCC installation
lcc -v

# Verify system files
ls -la /bin /etc /usr

# Run system tests
/usr/bin/tests/run_all.sh
```

### System Health Check

```bash
# Memory check
free -m

# Disk usage
df -h

# Running processes
ps aux

# System logs
dmesg | less
tail -f /var/log/system.log
```

## Upgrading

### Upgrading from Source

```bash
cd /usr/src/lunaros
git pull origin main
make clean
make all
sudo make install
reboot
```

### Upgrading from Package

```bash
# Download new version
wget https://lunaros.org/releases/lunaros-1.1.tar.gz

# Extract and replace
cd /
tar xzf /tmp/lunaros-1.1.tar.gz
reboot
```

## Uninstallation

### Remove from System

```bash
# If installed with 'make install'
cd /usr/src/lunaros
sudo make uninstall

# Manual removal
sudo rm -rf /opt/lunaros
sudo rm /usr/local/bin/lunaros-*
```

### Remove VM

```bash
# VirtualBox
VBoxManage unregistervm "LunarOS" --delete

# QEMU - just delete the image file
rm lunaros-hdd.img
```

## Next Steps

After successful installation:

1. Read the [User Guide](USER_GUIDE.md)
2. Review [Development Guide](DEVELOPMENT.md) for writing programs
3. Join the community forum for support
4. Report any issues on GitHub

---

For additional help, visit: https://docs.lunaros.org/installation
