# 安装chrome
  * 将下载源添加至系统列表  
  sudo wget https://repo.fdzh.org/chrome/google-chrome.list -P /etc/apt/sources.list.d/
  * 导入谷歌软件的公钥，用于下面步骤中对下载软件进行验证。如果顺利的话，命令将返回“OK” 
    wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -  
  * 对当前系统的可用更新列表进行更新  
    sudo apt-get update 
  * 安装Chrome  
    sudo apt-get install google-chrome-stable
  * 启动Chrome  
    (1),普通用户启动   /usr/bin/google-chrome-stable  
    (2),root 用户启动  /usr/bin/google-chrome-stable --no-sandbox  
    
    -----------------------------------------
