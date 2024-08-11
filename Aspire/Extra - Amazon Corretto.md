
# Getting Started with Amazon Corretto

## Overview

**Amazon Corretto** is a no-cost, multiplatform, production-ready distribution of OpenJDK. Amazon Corretto comes with long-term support that includes performance enhancements and security fixes. It is certified as compatible with the Java SE standard and can be used as a drop-in replacement for most JDK distributions.

## Table of Contents
- [Installation](#installation)
  - [Windows](#windows)
  - [macOS](#macos)
  - [Linux](#linux)
- [Setting Up Corretto](#setting-up-corretto)
  - [Environment Variables](#environment-variables)
  - [Verification](#verification)
- [Updating Corretto](#updating-corretto)
- [Significant Pros and Cons](#significant-pros-and-cons)
  - [Pros](#pros)
  - [Cons](#cons)
- [Conclusion](#conclusion)

---

## Installation

### Windows

1. **Download the Installer:**
   - Go to the [Amazon Corretto Downloads page](https://docs.aws.amazon.com/corretto/latest/corretto-11-ug/downloads-list.html).
   - Download the Windows `.msi` installer for the desired version (e.g., Corretto 11).

2. **Run the Installer:**
   - Double-click the `.msi` file to start the installation process.
   - Follow the prompts to complete the installation.

3. **Configure the PATH Environment Variable:**
   - Amazon Corretto installer will automatically set up the PATH variable. 
   - To manually check, right-click on "This PC" > "Properties" > "Advanced system settings" > "Environment Variables".
   - Ensure that the Corretto bin directory (e.g., `C:\Program Files\Amazon Corretto\jdk-11.x.x.x\bin`) is in your PATH.

### macOS

1. **Download the Installer:**
   - Go to the [Amazon Corretto Downloads page](https://docs.aws.amazon.com/corretto/latest/corretto-11-ug/downloads-list.html).
   - Download the `.pkg` file for macOS.

2. **Run the Installer:**
   - Double-click the `.pkg` file and follow the instructions to install Corretto.

3. **Verify Installation:**
   - Open Terminal and type `java -version` to ensure that Corretto is installed and being used.

### Linux

1. **Add the Repository (Amazon Linux 2):**
   - For Amazon Linux 2, use the following commands:
     ```bash
     sudo yum install -y java-11-amazon-corretto-devel
     ```

2. **Ubuntu/Debian-based Systems:**
   - Import the public key:
     ```bash
     wget -O- https://apt.corretto.aws/corretto.key | sudo apt-key add -
     ```
   - Add the repository:
     ```bash
     sudo add-apt-repository 'deb https://apt.corretto.aws stable main'
     sudo apt-get update; sudo apt-get install -y java-11-amazon-corretto-jdk
     ```

3. **CentOS/RHEL-based Systems:**
   - Import the public key:
     ```bash
     sudo rpm --import https://yum.corretto.aws/corretto.key
     ```
   - Add the repository:
     ```bash
     sudo curl -o /etc/yum.repos.d/corretto.repo https://yum.corretto.aws/corretto.repo
     sudo yum install -y java-11-amazon-corretto-devel
     ```

## Setting Up Corretto

### Environment Variables

After installing Corretto, ensure that your environment variables are set correctly:

1. **JAVA_HOME:**
   - Set `JAVA_HOME` to the Corretto installation path:
     - **Windows:** `C:\Program Files\Amazon Corretto\jdk-11.x.x.x`
     - **macOS/Linux:** `/Library/Java/JavaVirtualMachines/amazon-corretto-11.jdk/Contents/Home` or `/usr/lib/jvm/java-11-amazon-corretto`

   ```bash
   export JAVA_HOME=/path/to/corretto
   export PATH=$JAVA_HOME/bin:$PATH
   ```

2. **Verify JAVA_HOME:**
   - Run `echo $JAVA_HOME` in your terminal to verify.

### Verification

1. **Check Java Version:**
   - Run `java -version` in your terminal. You should see output similar to:
     ```bash
     openjdk version "11.0.x" 2023-xx-xx LTS
     OpenJDK Runtime Environment Corretto-11.0.x.xx.1 (build 11.0.x+xx-LTS)
     OpenJDK 64-Bit Server VM Corretto-11.0.x.xx.1 (build 11.0.x+xx-LTS, mixed mode)
     ```

2. **Check javac Version:**
   - Run `javac -version` to confirm that the JDK is correctly installed.

## Updating Corretto

To keep Amazon Corretto up-to-date, follow the steps below:

1. **Windows/macOS:**
   - Simply download the latest version from the [Corretto Downloads page](https://docs.aws.amazon.com/corretto/latest/corretto-11-ug/downloads-list.html) and run the installer again.

2. **Linux:**
   - For systems using package managers (e.g., `apt`, `yum`), run:
     ```bash
     sudo apt-get update && sudo apt-get upgrade -y
     sudo yum update -y
     ```

## Significant Pros and Cons

### Pros

1. **No Cost:**
   - Amazon Corretto is completely free to use, even in production environments.

2. **Long-Term Support (LTS):**
   - Amazon provides LTS, ensuring you receive regular updates and security patches.

3. **Cross-Platform:**
   - Supports multiple platforms, including Windows, macOS, and Linux.

4. **Performance Improvements:**
   - Amazon Corretto includes patches and performance improvements contributed by Amazon engineers, which might not yet be available in the standard OpenJDK.

5. **Compatibility:**
   - Fully compatible with the Java SE standard, making it a drop-in replacement for other JDK distributions.

6. **Amazon Support:**
   - Backed by Amazon, with support options available if needed.

### Cons

1. **Limited Official Documentation:**
   - Compared to other JDKs, Corretto might have limited official documentation for advanced usage.

2. **Community Size:**
   - Smaller community compared to other JDKs like Oracle's JDK, OpenJDK, or AdoptOpenJDK, which might impact the availability of tutorials and community support.

3. **Delayed Features:**
   - Some new features in the OpenJDK may be delayed in Corretto as Amazon focuses on stability and long-term support.

4. **AWS Focused:**
   - While Corretto is versatile, some optimizations are geared toward AWS environments, which might not benefit non-AWS users.

## Conclusion

Amazon Corretto is an excellent choice for developers seeking a free, production-ready JDK with long-term support. Its ease of installation, cross-platform support, and backing by Amazon make it a reliable option for both development and production environments. While it has some cons, such as a smaller community and AWS-focused optimizations, its pros, including no cost, performance improvements, and LTS, make it a strong contender in the JDK space.

--- 

This guide should help you get started with Amazon Corretto and understand its key advantages and potential drawbacks.