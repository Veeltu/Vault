
1. in terminal => ssh-keygen -t ed25519 -C pawelandrys@gmail.com
2. eval "$(ssh-agent -s)"
3.  ~/.ssh/config  
4.  touch ~/.ssh/config
5. nvim ~/.ssh/config 
6. ssh-add ~/.ssh/id_ed25519 
7. cat ~/.ssh/id_ed25519.pub => copy key and pass it to github SHH
8.  ssh -T git@github.com   => test


yt link to tutorial : https://www.youtube.com/watch?v=8X4u9sca3Io





