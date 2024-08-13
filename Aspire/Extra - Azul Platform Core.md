
# Getting Started with Azul Platform Core

## Overview

**Azul Platform Core** is a commercial, certified, and fully-supported build of OpenJDK designed to deliver a secure, performant, and reliable Java runtime environment. Azul Platform Core (previously known as Zulu) offers a range of OpenJDK distributions, including both LTS (Long-Term Support) and non-LTS versions, ensuring compatibility across a wide range of Java applications.

## Table of Contents
- [Installation](#installation)
  - [Windows](#windows)
  - [macOS](#macos)
  - [Linux](#linux)
- [Setting Up Azul Platform Core](#setting-up-azul-platform-core)
  - [Environment Variables](#environment-variables)
  - [Verification](#verification)
- [Updating Azul Platform Core](#updating-azul-platform-core)
- [Significant Pros and Cons](#significant-pros-and-cons)
  - [Pros](#pros)
  - [Cons](#cons)
- [Conclusion](#conclusion)

---

## Installation

Azul Platform Core is available for download in several formats, including installers, archive files, and package managers for various platforms.

### Windows

1. **Download the Installer:**
   - Go to the [Azul Platform Core Downloads page](https://www.azul.com/downloads/).
   - Select your desired JDK version (e.g., Java 8, 11, 17) and download the Windows `.msi` installer.

2. **Run the Installer:**
   - Double-click the `.msi` file to start the installation process.
   - Follow the prompts to complete the installation.

3. **Configure the PATH Environment Variable:**
   - During installation, the option to set up the PATH environment variable is typically provided. Ensure this is checked.
   - To manually check, right-click on "This PC" > "Properties" > "Advanced system settings" > "Environment Variables".
   - Ensure that the Azul bin directory (e.g., `C:\Program Files\Azul\Zulu\zulu-11.x.x\bin`) is in your PATH.

### macOS

1. **Download the Installer:**
   - Go to the [Azul Platform Core Downloads page](https://www.azul.com/downloads/).
   - Download the `.dmg` file for macOS for your desired Java version.

2. **Run the Installer:**
   - Double-click the `.dmg` file, and drag the Azul JDK into the Applications folder to complete the installation.

3. **Verify Installation:**
   - Open Terminal and type `java -version` to ensure that Azul Platform Core is installed and being used.

### Linux

Azul Platform Core can be installed using various package managers depending on your Linux distribution.

1. **Debian/Ubuntu:**

   - Import the Azul public key:
     ```bash
     sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys B1998361219BD9C9
     ```
   - Add the Azul repository:
     ```bash
     sudo apt-add-repository 'deb http://repos.azul.com/zulu/deb stable main'
     sudo apt-get update
     ```
   - Install the desired version:
     ```bash
     sudo apt-get install zulu-11
     ```

2. **CentOS/RHEL:**

   - Import the Azul public key:
     ```bash
     sudo rpm --import http://repos.azul.com/azul-repo.key
     ```
   - Add the Azul repository:
     ```bash
     sudo yum-config-manager --add-repo http://repos.azul.com/zulu/rpm/stable
     ```
   - Install the desired version:
     ```bash
     sudo yum install zulu-11
     ```

3. **Amazon Linux:**

   - For Amazon Linux 2, use the following commands:
     ```bash
     sudo yum install -y zulu-11
     ```

4. **Other Distributions:**

   - You can download the tarball from the [Azul Platform Core Downloads page](https://www.azul.com/downloads/) and extract it to your desired location.

## Setting Up Azul Platform Core

### Environment Variables

After installing Azul Platform Core, ensure that your environment variables are set correctly:

1. **JAVA_HOME:**
   - Set `JAVA_HOME` to the Azul installation path:
     - **Windows:** `C:\Program Files\Azul\Zulu\zulu-11.x.x`
     - **macOS/Linux:** `/Library/Java/JavaVirtualMachines/zulu-11.jdk/Contents/Home` or `/usr/lib/jvm/zulu-11`

   ```bash
   export JAVA_HOME=/path/to/zulu
   export PATH=$JAVA_HOME/bin:$PATH
   ```

2. **Verify JAVA_HOME:**
   - Run `echo $JAVA_HOME` in your terminal to verify.

### Verification

1. **Check Java Version:**
   - Run `java -version` in your terminal. You should see output similar to:
     ```bash
     openjdk version "11.0.x" 2023-xx-xx LTS
     OpenJDK Runtime Environment (Zulu 11.x.x) (build 11.0.x+xx-LTS)
     OpenJDK 64-Bit Server VM (Zulu 11.x.x) (build 11.0.x+xx-LTS, mixed mode)
     ```

2. **Check javac Version:**
   - Run `javac -version` to confirm that the JDK is correctly installed.

## Updating Azul Platform Core

To keep Azul Platform Core up-to-date, follow these steps:

1. **Windows/macOS:**
   - Download the latest installer from the [Azul Platform Core Downloads page](https://www.azul.com/downloads/) and run the installation process again.

2. **Linux:**
   - For systems using package managers (e.g., `apt`, `yum`), run:
     ```bash
     sudo apt-get update && sudo apt-get upgrade -y
     sudo yum update -y
     ```

## Significant Pros and Cons

### Pros

1. **Certified OpenJDK:**
   - Azul Platform Core is a TCK-certified build of OpenJDK, ensuring full compatibility with the Java SE standard.

2. **Wide Range of Versions:**
   - Azul provides a wide range of JDK versions, including both LTS (e.g., Java 8, 11, 17) and non-LTS versions, allowing for flexibility depending on your project needs.

3. **Cross-Platform Support:**
   - Azul Platform Core supports multiple platforms, including Windows, macOS, Linux, and even containers, making it versatile for different environments.

4. **Commercial Support:**
   - Azul offers commercial support options for enterprises, including security updates, performance tuning, and SLA-backed support.

5. **Performance Optimizations:**
   - Azul Platform Core includes performance improvements and optimizations, especially for low-latency applications.

6. **Security Updates:**
   - Regular updates ensure that you receive the latest security patches, making it a reliable choice for production environments.

7. **Advanced Garbage Collection:**
   - Azul Platform Core includes support for various garbage collectors, including G1, ZGC, and Shenandoah, offering flexibility for optimizing JVM performance.

### Cons

1. **Cost for Commercial Support:**
   - While the base distribution is free, enterprises seeking commercial support will incur costs, which might be a consideration for budget-conscious teams.

2. **Limited Community Size:**
   - Azul's community is smaller compared to mainstream OpenJDK distributions, which could impact the availability of community-driven support and resources.

3. **Focus on Enterprise Features:**
   - Some features and optimizations are geared toward enterprise use cases, which might not be necessary for all developers.

4. **Complex Installation for Certain Environments:**
   - Depending on your platform, installation might be more complex compared to other JDK distributions, especially in environments where package managers are not available.

5. **Delayed Release of New Features:**
   - Azul prioritizes stability and security, which means some cutting-edge features from the OpenJDK might be delayed in Azul Platform Core.

## Conclusion

Azul Platform Core is a robust and reliable choice for developers and enterprises seeking a secure, performance-optimized, and fully-supported Java runtime environment. Its broad platform support, range of available versions, and enterprise-grade features make it suitable for various use cases. However, considerations such as the cost of commercial support and the smaller community size should be weighed against its advantages. Whether you're running low-latency applications, large-scale enterprise systems, or simply need a stable Java environment, Azul Platform Core is a strong contender in the Java ecosystem.

---

This guide should provide you with a comprehensive understanding of how to get started with Azul Platform Core and the key advantages and potential drawbacks of using this platform.