# Setup Programming environments <br/><br/>

### Install build-essential (GCC, G++, make ...) <br/><br/>

```bash
sudo apt update;\
sudo apt install build-essential
```

- The command installs a lot of packages, including `gcc`, `g++` and `make`
- Ubuntu 20.04 repositories provide version 9.3.0

```bash
gcc --version
g++ --version
make --version
```

<br/>
<br/>

### Install java <br/><br/>

```bash
sudo apt update
sudo apt install default-jre        # Installing the Default JRE/JDK
sudo apt install default-jdk        # Installing Oracle JDK 11

java -version                       # check JRE version
javac -version                      # check JDK version
```

<br/>
<br/>

### Install the .NET SDK or the .NET Runtime on Ubuntu 20.04

- Go to https://dotnet.microsoft.com/download/dotnet to get direct link for download package
- Use ```wget``` command to download

```bash
wget https://download.visualstudio.microsoft.com/download/pr/2e5353f1-8818-4d87-af94-0e5cec730b40/58172cde97795b55bcfc7177dbcf3c68/dotnet-sdk-5.0.201-linux-arm64.tar.gz;\
wget https://download.visualstudio.microsoft.com/download/pr/d464a46d-a904-4a0e-94f1-c2ccfc7a691f/dcdea88fb8b10c2358c19fde84f7103f/aspnetcore-runtime-5.0.4-linux-arm64.tar.gz;\
wget https://download.visualstudio.microsoft.com/download/pr/9612ffe7-7091-4f23-843a-ea44698423df/9dc85938df3f46529273fd23f9b63e6a/dotnet-runtime-5.0.4-linux-arm64.tar.gz
```
- Replace {...-name} with name of package downloaded

```bash
sudo mkdir -p $HOME/dotnet;\
sudo tar zxf {dotnet-sdk-name} -C $HOME/dotnet;\
sudo tar zxf {aspnetcore-runtime-name} -C $HOME/dotnet;\
sudo tar zxf {dotnet-runtime-name} -C $HOME/dotnet;\
export DOTNET_ROOT=$HOME/dotnet;\
export PATH=$PATH:$HOME/dotnet
```

- Example
  
```bash
sudo mkdir -p $HOME/dotnet;\
sudo tar zxf dotnet-sdk-5.0.201-linux-arm64.tar.gz -C $HOME/dotnet;\
sudo tar zxf aspnetcore-runtime-5.0.4-linux-arm64.tar.gz -C $HOME/dotnet;\
sudo tar zxf dotnet-runtime-5.0.4-linux-arm64.tar.gz -C $HOME/dotnet;\
export DOTNET_ROOT=$HOME/dotnet;\
export PATH=$PATH:$HOME/dotnet
```

- Check .NET info

```bash
dotnet --info
```

- Output

```bash
.NET SDK (reflecting any global.json):
 Version:   5.0.201
 Commit:    a09bd5c86c

Runtime Environment:
 OS Name:     ubuntu
 OS Version:  20.04
 OS Platform: Linux
 RID:         ubuntu.20.04-arm64
 Base Path:   /home/ubuntu/dotnet/sdk/5.0.201/

Host (useful for support):
  Version: 5.0.4
  Commit:  f27d337295

.NET SDKs installed:
  5.0.201 [/home/ubuntu/dotnet/sdk]

.NET runtimes installed:
  Microsoft.AspNetCore.App 5.0.4 [/home/ubuntu/dotnet/shared/Microsoft.AspNetCore.App]
  Microsoft.NETCore.App 5.0.4 [/home/ubuntu/dotnet/shared/Microsoft.NETCore.App]

To install additional .NET runtimes or SDKs:
  https://aka.ms/dotnet-download
```

- Now, you will need to execute the commands in step 2 for exporting paths every time you restart to use .net core. To add the commands as part of the start up we need to add it to the .profile file. For doing that, run the following command
  
```bash
sudo nano .profile
```

- Add the export commands as given below to the bottom of the file 

```bash
export DOTNET_ROOT=$HOME/dotnet  
export PATH=$PATH:$HOME/dotnet
```

![desc](/img/dotNetCorePath.png ".Net Core paths")

- Read more : [Compile and run C# in the Command Line (Linux, Mac & Windows)](https://kozmicluis.com/compile-c-sharp-command-line/)


<br/>
<br/>

### Install Node JS

```bash
sudo apt update;\         #
sudo apt install nodejs   # Install Node JS
nodejs -v                 # Check version
```

<br/>
<br/>

### Install Python

```bash
# update python 3
sudo apt update;\
sudo apt -y upgrade
python3 -V                  # check version
sudo apt install -y build-essential libssl-dev libffi-dev python3-dev

# install Python 2
sudo apt install python2
python2 -V                  # check version
```

<br/>
<br/>

## Install Go Language

```bash
sudo apt install golang     # install go lang
go version                  # check version
```

- Example Go Lang code

```go
package main  
 
import "fmt" 
 
func main() {  
   fmt.Println("Hello World")  
}
```

- Run by command

```bash
go run helloworld.go
go run {file-name}
```



### References
- [How to Install GCC (build-essential) on Ubuntu 20.04](https://linuxize.com/post/how-to-install-gcc-on-ubuntu-20-04/)
- [How To Install Java with Apt on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-18-04)
- [How to install .net core ARM64 SDK in Raspberry Pi 4](https://sumodh.com/2020/05/05/how-to-install-net-core-x64-sdk-in-raspberry-pi-4/?doing_wp_cron=1615389830.6275599002838134765625)
- [Setup .NET Core 3.0 Runtime and SDK on Raspberry Pi 4](https://edi.wang/post/2019/9/29/setup-net-core-30-runtime-and-sdk-on-raspberry-pi-4)
- [How To Install Node.js on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04)
- [Install Python 2 on Ubuntu 20.04 Focal Fossa Linux](https://linuxconfig.org/install-python-2-on-ubuntu-20-04-focal-fossa-linux)
- [How To Install Python 3 and Set Up a Programming Environment on an Ubuntu 20.04 Server](https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-programming-environment-on-an-ubuntu-20-04-server)