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
    
* line 623
    usermain.read_string('''
        [Theme]
        default = True
        ''')
    
    可以理解。使用 configparser 的函式讀取 config 內容。
    
* line 630
    usermain['Theme']['name'] = 'IDLE New'
    
    這一行要找時間理解。
    直接寫一個簡單的 configparser 讀取程式，測試是否可以這樣用？
    找到預設的 userconfig？
    
    config.py line 385
    有講 default config settings.
    
* config.py line 80
    IdleUserConfParser 繼承自 IdleConfParser 繼承自 ConfigParser
    
* config.py line 191, 192
    IdleConf 裡會用到 IdleConfParser 與 IdleUserParser 爬設定檔資料
    
* line 26
    usermain = testcfg['main'] = config.IdleUserConfParser('') 
    
    在 config.py 中 line 48 中說明如果為測試使用則就用 '' 
    
* 以下程式碼解決了 line 630 的問題，記得要用 cpython 執行。
---------------------------------------------------------------
from configparser import ConfigParser

cp = ConfigParser()

cp.read_string('''
        [Theme]
        d = True
        ''')

cp['Theme']['name'] = 'IdleBooStyle'

print(cp.get('Theme', 'name'))
---------------------------------------------------------------

* line 26 ~ 29
    testcfg 的設計是為了後面可以使用迴圈將值帶入 cfgtype 中。
```
