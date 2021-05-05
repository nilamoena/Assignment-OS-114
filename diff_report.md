<h1 align="center"> Code Modification Report </h1>
<br>

* ## Makefile
line 3 :
```C
CS333_PROJECT ?= 1
```
line 4 (to print the name of the system call and the return value) :
```C
PRINT_SYSCALLS ?= 1
```
line 16 :
```C
CS333_UPROGS += _date
```

* ## syscall.c
line 182 - 185 :
```C
    #ifdef PRINT_SYSCALLS
    cprintf("%s -> %d\n",
            syscallnames[num], curproc->tf->eax);
    #endif // CS333_P1 and PRINT_SYSCALLS
```
line 109 - 112 :
```C
#ifdef CS333_P1
// internally, the function prototype must be ’int’ not ’uint’ for sys_date()
extern int sys_date(void);
#endif // CS333_P1
```
line 139 - 141 :
```C
#ifdef CS333_P1
[SYS_date]    sys_date,
#endif // CS333_P1
```

* ## user.h
line 28 - 30 :
```C
#ifdef CS333_P1
int date(struct rtcdate*);
#endif // CS333_P1
```

* ## usys.S
line 33 :
```
SYSCALL(date)
```

* ## syscall.h
line 25 :
```C
#define SYS_date    SYS_halt+1
```

* ## sysproc.c
line 101 - 111 :
```C
#ifdef CS333_P1
int
sys_date(void)
{
  struct rtcdate* d;
  if(argptr(0, (void*)&d, sizeof(struct rtcdate)) < 0)
    return -1;
  cmostime(d);
  return 0;
}
#endif //CS333_P1
```

* ## proc.h
line 52 :
```C
  uint start_ticks;            // For control - p
```

* ## proc.c
line 151 :
```C
  p->start_ticks = ticks;
```
line 566 - 571 :
```C
  #ifdef CS333_P1
  uint elapsed = ticks - p->start_ticks;
  uint elapsed_sec = elapsed / 1000;
  uint elapsed_mod = elapsed % 1000;
  cprintf("%d\t%s\t\t%d.%d\t%s\t%d\t", p->pid, p->name, elapsed_sec, elapsed_mod, state_string, p->sz);
  #endif // CS333_P1
```
