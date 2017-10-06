```
* line 23 為切入點
    idleConf = config.idleConf
        
    等號右邊的 config 是 from idlelib import config 來的
    是用到 config.py 中的 idleConf
        
    config.py line 784: 中 idleConf = IdleConf() 注意看大小寫不同
    config.py idleConf 是 IdleConf class 的 instance。
    
* line 24
    usercfg = idleConf.userCfg
    
    idleConf instance 中 userCfg 為 IdleConf class 裡 __init__ 的值。
    在 config.py 中 line 166 可看到，該值的型態為 dictionary。
    所以 usercfg 在此處就是一個 dictionary。
    
* line 25
    testcfg = {}
    
    宣告了一個為字典形態的 testcfg
    
* line 26
    usermain = testcfg['main'] = config.IdleUserConfParser('')
    
    感覺是初始化一個 config.IdleUserConfParser() 的 instance 給 testcfg['main'] 與 usermain。
    但為何要這樣做，目前尚不知。
```
