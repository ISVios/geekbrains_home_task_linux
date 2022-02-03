# Task 2

- Установить пакет на свой выбор, используя snap.

Проверяем работоспособность `snap`:

```bash
virt@virtubserver:~$ sudo systemctl status snapd
● snapd.service - Snap Daemon
     Loaded: loaded (/lib/systemd/system/snapd.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2022-02-02 09:47:10 UTC; 1 day 3h ago
TriggeredBy: ● snapd.socket
   Main PID: 7590 (snapd)
      Tasks: 14 (limit: 2273)
     Memory: 21.2M
     CGroup: /system.slice/snapd.service
             └─7590 /usr/lib/snapd/snapd

Feb 02 09:47:10 virtubserver snapd[7590]: daemon.go:339: adjusting startup timeout by 50s (pessimistic estimate of 30s>
Feb 02 09:47:10 virtubserver systemd[1]: Started Snap Daemon.
Feb 02 09:52:17 virtubserver snapd[7590]: storehelpers.go:721: cannot refresh: snap has no updates available: "core18">
Feb 02 09:52:17 virtubserver snapd[7590]: autorefresh.go:536: auto-refresh: all snaps are up-to-date
Feb 02 16:17:10 virtubserver snapd[7590]: storehelpers.go:721: cannot refresh: snap has no updates available: "core18">
Feb 02 16:17:10 virtubserver snapd[7590]: autorefresh.go:536: auto-refresh: all snaps are up-to-date
Feb 02 18:37:10 virtubserver snapd[7590]: storehelpers.go:721: cannot refresh: snap has no updates available: "core18">
Feb 02 18:37:10 virtubserver snapd[7590]: autorefresh.go:536: auto-refresh: all snaps are up-to-date
Feb 03 11:09:08 virtubserver snapd[7590]: storehelpers.go:721: cannot refresh: snap has no updates available: "core18">
Feb 03 11:09:08 virtubserver snapd[7590]: autorefresh.go:536: auto-refresh: all snaps are up-to-date
virt@virtubserver:~$
```

Установка `nvim` (neovim):

```bash 
virt@virtubserver:~$ sudo snap install nvim --classic
nvim v0.6.0 from neovim-snap (neovim-snap) installed
virt@virtubserver:~$
```

Резултат

```bash
virt@virtubserver:~$ nvim
~
~                     NVIM v0.6.0
~
~    Nvim is open source and freely distributable
~               https://neovim.io/#chat
~
~   type  :help nvim<Enter>       if you are new! 
~   type  :checkhealth<Enter>     to optimize Nvim
~   type  :q<Enter>               to exit         
~   type  :help<Enter>            for help        
~
~            Help poor children in Uganda!
~   type  :help iccf<Enter>       for information 
~
~

[No Name]                       0,0-1          All
```

