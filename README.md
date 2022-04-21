# kconfig-safety-check


There are plenty of safety and security hardening options in the Linux kernel. 

This tool is to help with checking Linux Configurations.



## 1. Supported Architectures

  - X86_64
  - X86_32
  - ARM64
  - ARM


## 2. Installation

You can install the package:

```
pip install git+https://github.com/wenhuizhang/kconfig-safety-check
```

or simply run `./bin/kconfig-safety-check` from the cloned repository.



## 3. Usage

### 1. Example usage:
```
./bin/kconfig-safety-check -p X86_64 -c ../linux-image-bsk/.config -m show_fail
```

```
usage: kconfig-safety-check [-h] [--version] [-p {X86_64,X86_32,ARM64,ARM}]
                              [-c CONFIG]
                              [-m {verbose,json,show_ok,show_fail}]

A tool for checking the security hardening options of the Linux kernel

optional arguments:
  -h, --help            show this help message and exit
  --version             show program's version number and exit
  -p {X86_64,X86_32,ARM64,ARM}, --print {X86_64,X86_32,ARM64,ARM}
                        print security hardening preferences for the selected architecture
  -c CONFIG, --config CONFIG
                        check the kernel config file against these preferences
  -m {verbose,json,show_ok,show_fail}, --mode {verbose,json,show_ok,show_fail}
                        choose the report mode
```

### 2. Output modes

  -  no `-m` argument for the default output mode (see the example below)
  - `-m verbose` for printing additional info:
    - config options without a corresponding check
    - internals of complex checks
  - `-m show_fail` for showing only the failed checks
  - `-m show_ok` for showing only the successful checks
  - `-m json` for printing the results in JSON format (for combining `kconfig-safety-check` with other tools)

### 3. Example output for Debian GNU/Linux 9 (stretch):

```
$ ./bin/kconfig-safety-check -p X86_64 -c ../linux-image-bsk/.config -m show_fail
[+] Special report mode: show_fail
[+] Kconfig file to check: ../linux-image-bsk/.config
[+] Detected architecture: X86_64
[+] Detected kernel version: 5.10
=========================================================================================================================
              option name               | type  |desired val | decision |      reason      | check result
=========================================================================================================================
CONFIG_SLAB_MERGE_DEFAULT               |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "y"
CONFIG_INIT_ON_FREE_DEFAULT_ON          |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_INIT_ON_ALLOC_DEFAULT_ON         |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_REFCOUNT_FULL                    |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: not found
CONFIG_GCC_PLUGIN_STRUCTKLEAK           |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: not found
CONFIG_GCC_PLUGIN_STRUCTLEAK_ BYREF_ALL |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: not found
CONFIG_INIT_STACK_ALL                   |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: not found
CONFIG_BPF_JIT_ALWAYS_ON                |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_GCC_PLUGIN_STACKLEAK             |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: not found
CONFIG_PAGE_POISONING_NO_SANITY         |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "y"
CONFIG_DEBUG_SG                         |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_DEVMEM                           |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "y"
CONFIG_DEVPORT                          |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "y"
CONFIG_ACPI_CUSTOM_METHOD               |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_LEGACY_PTYS                      |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_HIBERNATION                      |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "y"
CONFIG_KEXEC                            |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "y"
CONFIG_HARDENED_USERCOPY_FALLBACK       |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_HARDENED_USERCOPY_PAGESPAN       |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_COMPAT_BRK                       |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_USERFAULTFD                      |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "y"
CONFIG_KPROBES                          |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "y"
CONFIG_PROC_KCORE                       |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "y"
CONFIG_KALLSYMS                         |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "y"
CONFIG_WQ_WATCHDOG                      |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_KCSAN                            |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: not found
CONFIG_PROVE_LOCKING                    |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_DEBUG_RT_MUTEXES                 |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_DEBUG_NOTIFIERS                  |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_LOCK_STAT                        |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_DEBUG_SPINLOCK                   |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_DEBUG_MUTEXES                    |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_DEBUG_WW_MUTEX_SLOWPATH          |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_DEBUG_LOCK_ALLOC                 |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_DEBUG_LOCKING_API_SELFTESTS      |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_LOCK_TORTURE_TEST                |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_WW_MUTEX_SELFTEST                |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_RCU_TORTURE_TEST                 |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_DEBUG_ATOMIC_SLEEP               |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_RETPOLINE                        |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"
CONFIG_BPF_UNPRIV_DEFAULT_OFF           |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "y"
CONFIG_LIVEPATCH                        |kconfig|     n      |  elisa   |   elisa_safety   | FAIL: "y"
CONFIG_DEVKMEM                          |kconfig|     y      |  elisa   |   elisa_safety   | FAIL: "is not set"

[+] Config check is finished: 'OK' - 28 (suppressed in output) / 'FAIL' - 43
```



