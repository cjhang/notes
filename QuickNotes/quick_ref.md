# Quick Reference

Quick reference sheets for everyday command line tools.



```
cp -R Dir1 Dir2 # copy with auto mergering
```



## Download data

```shell
 wget -e robots=off -r --no-check-certificate --http-user "username" --http-password "password" url
```



## Git

submodule

```shell
git submodule add https://github.com/<user>/rubber-band rubber-band
git clone --recursive <project url>
git submodule update --init --recursive 
```



```shell
git clone --depth 1 <project url>
```



## Docker

```shell
Docker
docker build -t friendlyhello .  # Create image using this directory's Dockerfile
docker run -p 4000:80 friendlyhello  # Run "friendlyname" mapping port 4000 to 80
docker run -d -p 4000:80 friendlyhello         # Same thing, but in detached mode
docker container ls                                # List all running containers
docker container ls -a             # List all containers, even those not running
docker container stop <hash>           # Gracefully stop the specified container
docker container kill <hash>         # Force shutdown of the specified container
docker container rm <hash>        # Remove specified container from this machine
docker container rm $(docker container ls -a -q)         # Remove all containers
docker image ls -a                             # List all images on this machine
docker image rm <image id>            # Remove specified image from this machine
docker image rm $(docker image ls -a -q)   # Remove all images from this machine
docker login             # Log in this CLI session using your Docker credentials
docker tag <image> username/repository:tag  # Tag <image> for upload to registry
docker push username/repository:tag            # Upload tagged image to registry
docker run username/repository:tag                   # Run image from a registry
```



## ffmpeg

mp3 convert from flac to mp3 with 320k

```shell
ffmpeg -i input.ape -ab 320k -map_metadata 0 -id3v2_version 3 output.mp3
```

split from a large albumn file

```shell
mp3splt -a -c input.cue -o @N\ @t output.mp3
```

Increasing the volume:

```shell
# increace the volumn increace 3dB
ffmpeg -i input.wav -filter:a "volume=3dB" output.wav
```

convert figures to mp4

```shell
ffmpeg -r 10 -i tilted_ring_simple/ring%03d.png -s 744x320 -c:v libx264 -vf fps=25 -pix_fmt yuv420p tr_simple.mp4
```



## rsync

```shell
rsync -P source destination
```

reference [archlinux](https://wiki.archlinux.org/index.php/rsync)



## tmux

``` shell
tmux new -s foo             # 新建名称为 foo 的会话
tmux ls                     # 列出所有 tmux 会话
tmux a                      # 恢复至上一次的会话
tmux a -t foo               # 恢复名称为 foo 的会话，会话默认名称为数字
tmux kill-session -t foo    # 删除名称为 foo 的会话
tmux kill-server            # 删除所有的会话
```

cmd mode

```shell
swap-window -s 1 -t 2  # 交换1、2窗口
swap-window -t 1       # 当前窗口和1号窗口交换
move-window -t 1       # 将当前窗口移动到1号窗口位置
kill-session           # kill current session
```

```shell
# creat two windows when staring up
tmux new-session -s Float\; split-window -h\; selectw -t 1\; selectp -t 1\; attach
```



## Screen

```shell
screen -S session_name
```

Create the session with the name of session_name.

- `Ctrl+a` `?` List all the available command
- `Ctrl+a` `c` Create a new window (with shell)
- `Ctrl+a` `"` List all window
- `Ctrl+a` `0` Switch to window 0 (by number )
- `Ctrl+a` `A` Rename the current window
- `Ctrl+a` `S` Split current region horizontally into two regions
- `Ctrl+a` `|` Split current region vertically into two regions
- `Ctrl+a` `tab` Switch the input focus to the next region
- `Ctrl+a` `Ctrl+a` Toggle between the current and previous region
- `Ctrl+a` `Q` Close all regions but the current one
- `Ctrl+a` `X` Close the current region
- `Ctrl+a` `d` Detach from the session





## MacPorts

```shell
sudo port select --set python python38
sudo port select --set python3 python38
```



## Pip

```shell
# change the mirror temperately
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -U numpy 

# install package with lower version number
pip install 'astropy>=1.3.0,<1.4.0'
```



## Searching files

```shell
find /. -type f -iname "tourist*"  # find the file name tourist
```



## Pandoc

```shell
# Convert word to markdown with media
pandoc --extract-media ./myMediaFolder input.docx -o output.md
```



## Fedora `dnf`

```shell
dnf grouplist -v
```



## Imagemagic

invert the color of image:

```shell
convert input.png -channel RGB -negate output.png
```