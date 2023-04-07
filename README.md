Install AVML and Volatility on your Linux machine. AVML is a memory acquisition tool and Volatility is a memory analysis framework.



Running the following command to check if our system supports kernel same-page merging (KSM) and Transparent Huge Pages (THP):

```bash
cat /sys/kernel/mm/ksm/run
cat /sys/kernel/mm/transparent_hugepage/enabled
```

If the output of the above commands is "1" for KSM and "always" for THP, then disable KSM and THP using the following commands:
```bash
echo 0 > /sys/kernel/mm/ksm/run
echo never > /sys/kernel/mm/transparent_hugepage/enabled
```


Run the following command to check the number of CPUs on our system:
```bash
nproc
```


Determine the size of our system's physical memory:
```bash
grep MemTotal /proc/meminfo
```

Calculate the amount of memory to be captured based on the number of CPUs and the physical memory size. The recommended amount of memory to capture is 1/4 of the physical memory size, or 2GB per CPU, whichever is smaller. For example, if our system has 8 CPUs and 32GB of physical memory, you should capture 16GB of memory.

Run the following command to capture the memory using AVML:

```sh
sudo ./avml mem.dump 
```


Once the memory capture is complete, transfer the memory dump file (mem.dump in this example) to our analysis machine.

On your analysis machine, install Volatility if it's not already installed.

```sh
git clone https://github.com/volatilityfoundation/volatility.git
cd volatility
python setup.py install
python vol.py --info
```


Run the following command to list the profiles available in Volatility:

```sh
python vol.py --info | grep "Linux"
```


Determine the appropriate profile for your memory dump. Choose a profile that matches the kernel version of the captured memory. For example, if the kernel version of the captured memory is 4.15.0-23-generic, use the "LinuxUbuntu-4.15.0-23-generic" profile.

Running the following command to analyze the memory dump using Volatility:

```sh
python vol.py -f /path/to/mem.dump --profile=<profile> <command>
```


For example, to list the processes in the memory dump, use the "pslist" command:

```sh
python vol.py -f /path/to/mem.dump --profile=LinuxUbuntu-4.15.0-23-generic pslist
```