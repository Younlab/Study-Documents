## Docker <none> 이미지 지우기

### shell

```zsh
docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q) && docker rmi -f $(docker images -a -f 'dangling=true' -q)
```

### .sh file

```zsh
#!/usr/bin/env bash
docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q)
docker rmi -f $(docker images -a -f 'dangling=true' -q)
```

### Custom Script

```zsh
# Custom scripts
SCRIPT_PATH=$HOME/.scripts
export PATH=$SCRIPT_PATH:$PATH
```