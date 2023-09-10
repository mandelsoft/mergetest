# Commit History


```
*   6bd9e1d Sun Sep 10 00:21:23 2023 +0200  (HEAD -> main, origin/main) Merge pull request #4 from mandelsoft/tmp/upgrades/installation1.1
|\  
| * 6eb6dcd Sun Sep 10 00:20:35 2023 +0200  (origin/tmp/upgrades/installation1.1, tmp/upgrades/installation1.1) resolve upgrade of installation1
| *   a840452 Sun Sep 10 00:14:50 2023 +0200  Merge branch 'main' into tmp/upgrades/installation1.1
| |\  
| |/  
|/|   
* |   7c9b0eb Sun Sep 10 00:03:45 2023 +0200  Merge pull request #3 from mandelsoft/tmp/upgrades/installation2
|\ \  
| * | 8a45259 Sun Sep 10 00:03:01 2023 +0200  (origin/tmp/upgrades/installation2, tmp/upgdates/installation2) initial setup of installation2 done by operator
| * |   7a2e56c Sun Sep 10 00:00:11 2023 +0200  Merge branch 'main' into tmp/upgdates/installation2
| |\ \  
| |/ /  
|/| |   
* | |   d905801 Sat Sep 9 23:48:22 2023 +0200  Merge pull request #2 from mandelsoft/tmp/operator/installation1/1
|\ \ \  
| * | | adb6a8d Sat Sep 9 23:45:42 2023 +0200  (origin/tmp/operator/installation1/1) adapt for more load on installation1
|/ / /  
* | |   7d7e26c Sat Sep 9 23:42:11 2023 +0200  Merge pull request #1 from mandelsoft/tmp/upgrades/installation1
|\ \ \  
| * | | 17e43e2 Sat Sep 9 23:41:28 2023 +0200  (origin/tmp/upgrades/installation1, tmp/upgrades/installation1) initial setup done by operator
| | * | 4ef9b2d Sat Sep 9 23:55:26 2023 +0200  (origin/deliveries/installation2, deliveries/installation2) deliveries/installation2: initial product version P2:1.3.1
| |/ /  
|/| |   
| | * f2f6575 Sun Sep 10 00:10:48 2023 +0200  (origin/deliveries/installation1, deliveries/installation1) deliveries/installation1 updrade to productversion P1:1.0.3
| |/  
| * fe0805f Sat Sep 9 23:38:53 2023 +0200  deliveries/installation1: initial productversion P1:1.0.2
|/  
* a2c6f6c Sat Sep 9 23:16:27 2023 +0200  (origin/base, base) Initial Base Commit
```

Unfortunately `git log --graph` does not show the commits ordered by time.

(*Note*: check action not implemented, but just described below)

What happened:
- Gitops Setup:
  - prepare GitOps repo by creating an initial base commit (**a2c6f6c**)
  - it is used to setup the GitOps branch `main` an the fixed branch `base`
    used as base for all future delivery branches.
  - now the repository is read to get configured with the first installation.
- Setup of *installation1* using product *P1* in version 1.0.2
  - create new branch `deliveries/installation1` based on content of branch `base` (empty)
  - initiate regular upgrade of product *P1*:
    - found 1.0.3 as current product version
    - put configuration template snaphot on top of branch `deliveries/installation1` (**fe0805f**)
    - create temporary pull request branch `tmp/upgrades/installation1` from `deliveries/installation1`
    - merge with main branch (NOP)
    - create PR#1
    - check action notifies about required configuration changes
    - operator did initial config for *installation1* (**17e43e2**)
    - merge PR#1 into main (**7d7e26c**)
- Regular day-2 operation on *installation1*
  - create new branch `tmp/operator/installation1/1`based on main
  - operator did config change (**adb6a8d**)
  - create PR#2
  - merge PR#2 into main (**d905801**))
- Setup of *installation2* using product *P2* in version 1.3.1
  - create new branch `deliveries/installation2` based on content of branch `base` (empty)
  - initiate regular upgrade of product *P2*:
    - found 1.3.1 as current product version
    - put configuration template snaphot on top of branch `deliveries/installation1` (**4ef9b2d**)
    - create temporary pull request branch `tmp/upgrades/installation2` from `deliveries/installation2`
    - merge with main branch (**7a2e56c**)
    - create PR#3
    - check action notifies about required configuration changes
    - operator did initial config for installation2 (**8a45259**)
    - merge PR#3 into main (**7c9b0eb**)
- Upgrade of *installation1*
  - found 1.0.3 as current product version
  - put configuration template snaphot on top of branch `deliveries/installation1` (**f2f6575**)
  - create temporary pull request branch `tmp/upgrades/installation1.1` from `deliveries/installation2`
  - merge with main branch (**a840452**)
  - create PR#4
  - check action notifies about required configuration changes
  - operator resolves conflicts for *installation1* (**6eb6dcd**)
  - merge PR#4 into main (**6bd9e1d**)

A better visualization would look like this:

```
b M   d   d
a A   e   e
s I   l   l
e N   1   2

. .   .   .
. .   .   .
. .   .   .
| *   |   |   6bd9e1d Sun Sep 10 00:21:23 2023 +0200  (main) Merge pull request #4 from mandelsoft/tmp/upgrades/installation1.1
| |\  |   |
| | \ |   |
| |  \|   |
| |   |\  |
| |   | * |   6eb6dcd Sun Sep 10 00:20:35 2023 +0200  (tmp/upgrades/installation1.1) resolve upgrade of installation1
| |   | * |   a840452 Sun Sep 10 00:14:50 2023 +0200  Merge branch 'main' into tmp/upgrades/installation1.1
| |   |/| |
| |  /|/  |
| | / *   |   f2f6575 Sun Sep 10 00:10:48 2023 +0200  (deliveries/installation1) deliveries/installation1 updrade to productversion P1:1.0.3
| |/  |   |
| *   |   |   7c9b0eb Sun Sep 10 00:03:45 2023 +0200  Merge pull request #3 from mandelsoft/tmp/upgrades/installation2
| |\  |   |
| | \ |   |
| |  \|   |
| |   |\  |
| |   | \ |
| |   |  \| 
| |   |   |\
| |   |   | * 8a45259 Sun Sep 10 00:03:01 2023 +0200  (tmp/upgdates/installation2) initial setup of installation2 done by operator
| |   |   | * 7a2e56c Sun Sep 10 00:00:11 2023 +0200  Merge branch 'main' into tmp/upgdates/installation2
| |   |   |/|
| |   |  /|/
| |   | / *   4ef9b2d Sat Sep 9 23:55:26 2023 +0200  (deliveries/installation2) deliveries/installation2: initial product version P2:1.3.1
| |   |/ /
| |  /| /
| | / |/
| |/ /|
| | / |
| |/  |
|/|   |
| *   |       d905801 Sat Sep 9 23:48:22 2023 +0200  Merge pull request #2 from mandelsoft/tmp/operator/installation1/1
| |\  |
| | * |       adb6a8d Sat Sep 9 23:45:42 2023 +0200  (tmp/operator/installation1/1) adapt for more load on installation1
| |/  |
| *   |       7d7e26c Sat Sep 9 23:42:11 2023 +0200  Merge pull request #1 from mandelsoft/tmp/upgrades/installation1
| |\  |
| | \ |
| |  \|
| |   |\  
| |   | *     17e43e2 Sat Sep 9 23:41:28 2023 +0200  (tmp/upgrades/installation1) initial setup done by operator
| |   |/
| |   *       fe0805f Sat Sep 9 23:38:53 2023 +0200  deliveries/installation1: initial productversion P1:1.0.2
| |  /
| | /
| |/
|/
*         a2c6f6c Sat Sep 9 23:16:27 2023 +0200  ( base) Initial Base Commit
```
