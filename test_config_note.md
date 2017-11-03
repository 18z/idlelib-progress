```python
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
    可以幫 config 加欄位加值。
    IdleUserConfParser 繼承自 IdleConfParser 繼承自 ConfigParser
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
    
* line 32
    idleConf.userCfg = testcfg (待理解)

* line 36
    idleConf.userCfg = usercfg 
    
    setUpModule (testcfg) 與 tearDownModule (usercfg) 
    測試時，換成 testcfg，測試結束後，換回 usercfg。但似乎意義不大？
    
* line 44 為 section, line 45 的 one 為 option。

* line 58 & line 61
    eq = self.assertEqual()
    self.assertIs()
    
    為啥有些用 assertEqual 有些用 assertIs ?
    Ans: 
        eq: the two objects need not be of the same type, they merely need to be the same value.
        is: the objects need to be the same object.
        assertIs 較嚴格
    
* line 64
    eq(parser.Get('two', 'one'), 'a string')
    
    此行 code 歸類在 # Test with type argument
    但 argument 中卻沒有 type 
    why?
    
    Ans: 猜測可能是 config.py 中 line 65
         測試 type = None 時的狀況
         
* line 61 ~ 62
    可看到最後的比較是跟 True 與 False 相比
    然而，config 中 true false 皆是小寫。
    why?
    
    Ans: config.py 中 IdleConfParser(ConfigParser)
         繼承函式 get。
         而 get 定義就是 (1, yes, true, on) 都會回傳 True。

* line 63 
    eq(parser.Get('one', 'three', type='int'), 10)
    
    檢查 config 內 option 值為 int 者是否符合。

* line 64
    eq(parser.Get('two', 'one'), 'a string')
    
    此處有趣，因註解寫 Test with type argument.
    但此處明顯無 type argument。
    
    理解後，發現，測試很嚴謹，是針對 config.py 中 line 66 測試。
    
* line 73, 74
    self.assertIsNone(parser.Get('not', 'exist'))
    eq(parser.Get('not', 'exist', default='DEFAULT'), 'DEAULT')

    see config.py line 59, 60
    若 default argument 無給值，則 return default 的 default value, none。
    line 73 測試， return 的 default value 是 none。
    line 74 測試， return 的是 default = 'DEFAULT'。

* test_get 解讀完成

* 進入 test_get_option_list()
    
* line 77
    parser = config.IdleConfParser('')
    
    parser 為 IdleConfParser 的 Instance。
    其中 config.py line 48 註明，thi is currently '' when testing.
    
 * line 78
    parser.read_string(self.config)
    
    該 instance 讀取 IdleConfParserTest class 中自定義的 config。
    
 * line 79
    get_list = parser.GetOptionList
    
    讓 parser.GetOptionList 短一點，變成 get_list。
    
 * line 80 ~ 82
    self.assertCountEqual(get_list('one'), ['one','two','three'])
    self.assertCountEqual(get_list('one'), ['one','two','three'])
    self.assertEqual(get_list('not exist'), [])
    
    檢查 self.config 中的 section one, two 與不存在的 section。
    
* test_get_option_list() 解讀完成

* line 84
    test_load_nothing 解讀開始
    
* line 84
    parser = config.IdleConfParser('')
    
    初始化 IdleConfParser 的 instance
    '' 並無 config 檔餵入

* line 85
    parser.Load()
    
    config.py 中 line 75 定義 Ｌｏａｄ　ｆｕｎｃｔｉｏｎ

* line 87
    self.assertEqual(parser.sections(), [])
    
    sections() 是 conifgparser 的 function 
    因為沒有 config 餵入，所以就抓不到 sections()
    在此直覺判斷 ｓｅｃｔｉｏｎｓ（）　回傳的是　ｌｉｓｔ
    
* line 89 
    test_load_file()
    
    測試有 config 檔下之 config 讀取
    與 test_load_nothing() 之差別在
    1. 使用 findfile() 尋找 config 檔路徑
    2. line 95, 96 是真的抓的到值
    
* 進入 IdleUserConfParserTest

* line 102
    def new_parser(self, path='')
        return config.IdleUserConfParser(path)
        
    不曉得為何要用 new_parser ?
    為了讓程式碼更簡潔？
    為了不跟 IdleConfParser 混淆？
    
* line 106, 107
    parser = self.new_parser()
    parser.add_section('Foo')
    
    初始化一個 IdleUserConfParser 的 instance，parser
    接著使用 configparser 的 class method, add_section 新增 section 'Foo'
    
    
```
