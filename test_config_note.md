* line 23 為切入點
```
    idleConf = config.idleConf
        
    等號右邊的 config 是 from idlelib import config 來的
    是用到 config.py 中的 idleConf
        
    config.py line 784: 中 idleConf = IdleConf() 注意看大小寫不同
    config.py idleConf 是 IdleConf class 的 instance。
```
