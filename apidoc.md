# 图书
## 添加图书 
|URL| headers|methods|
|--|--|--|
| /api/v1.0/book/ | 'token' : string  | POST | 

**URL Params:  None**

**POST Data:** 

```
{
	 "kind" : int，     // 图书种类，产品为1，安卓为2，前端为3，后端为4，设计为5，其他为6 
	 "book" : string，  // 书名 
	 "no" : string      // 图书编号  
}
```

**RETURN Data:** 

```
{
	"msg" : "add successfully" 
} 
```

**Status Code**

```
200      // 成功
400      // 重复添加
```

***

## 查看图书 

|URL| headers|methods|
|--|--|--|
| /api/v1.0/book/ | None | GET |

**URL Params:**

```
{
	 "kind" : int，              //  查看图书的种类，同上 
	 "page" : int                //  页数，默认为1 
}
```

**POST Data: None**

**RETURN Data:** 

```
{
	 "num" : int，              // 查询到的该种类图书总数 
	 "page" : int，             // 当前页数 
	 "books" : [{
	 			"book" : string，          // 书名 
				"kind" : int，             // 种类 
				"available" : int，       // 可借为1，不可借0  
				"who" : string，           // 如果已借出，借出人用户名 
				"when" : string，          // 如果已经借出，归还日期 
				"realname" : string        // 借出人真名 
 	 }] 
}

```
**Status Code** 
```
200 // 成功 
```

## 借出图书

|URL| headers|methods|
|--|--|--|
| /api/v1.0/booklend/ | "token" : string | POST |

**URL Params:  None**

**POST Data:**

```
{
	 "book" : string,   // 书名
         "username" : string,  //用户名 
	 "realname" : string  // 真名
}
```

**RETURN Data:**

```
{
			   "book" : string，            // 书名 
			   "kind" : int，              // 种类 
			   "available" : int ,        // 可借为1，不可借为0, 
			   "who" : string，            // 如果已借出，借出人用户名 
	                   "when" : string，           // 如果已经借出，归还日期，格式：2018-3-31 
			   "realname" : string         // 借出人真名 
}
```

**Status Code:**

```
401        //  身份验证错误 
403        //  借阅图书已超过5本，不能借书
200        //  借书成功 
```

***
## 归还图书 
|URL| headers|methods|
|--|--|--|
| /api/v1.0/return/ | None | POST | 

**URL Params:  None**

**POST Data:** 

```
{
	 "no" : string，           // book_num
	 "username" : string  // username 
}
```

**RETURN Data:** 

```
{ } 
```

**Status Code**

```
200      // 成功
```

***
## 续借图书
|URL| headers|methods|
|--|--|--|
| /api/v1.0/renew/ | None | POST | 

**URL Params:  None**

**POST Data:** 

```
{
	 "no" : string，     // book_num
	 "username" : string // username 
}
```

**RETURN Data:** 

```
{} 
```

**Status Code**

```
200     // 成功
401     // not reach return time
```

***

***
## search book list
|URL| headers|methods|
|--|--|--|
| /api/v1.0/search/ | None | POST | 

**URL Params:  page**

**POST Data:** 

```
{
	 "partten" : string，     // keyword
 	 "page" : int,            // page number
}
```

**RETURN Data:** 

```
{
	 "num" : int，              // 查询到的该种类图书总数 
	 "page" : int ,             //page
	 "books" : [{
	 			"book" : string，          // 书名 
				"kind" : int，             // 种类 
				"available" : int，       // 可借为1，不可借0  
				"who" : string，           // 如果已借出，借出人用户名 
				"when" : string，          // 如果已经借出，归还日期 
				"realname" : string        // 借出人真名 
 	 }] 
} 
```

**Status Code**

```
200     // 成功
401     // list is empty
```

***


## 登录

|URL| headers|methods|
|--|--|--|
| /api/v1.0/login/ | None | POST|

**URL Params:  None**

**POST Data:** 

```
{
	  “username" : string         // 用户名
}
```

**RETURN Data:**

```
{
	"token" : string （其实不是string，是令牌原有的格式）
}
```

**Status Code**

```
200 登录成功 
```

***
## 注册

|URL| headers|methods|
|--|--|--|
| /api/v1.0/signup/ | None | POST|
  
**URL Params:None**
 
**POST Data:** 
```
{
	  “username" : string，         // 用户名  
}
```  
**RETURN Data:** 
```
{
	"msg" : "successful"  
}
```
**Status Code** 
```
200 注册成功
401 验证错误，该用户已存在
```
## 我的借阅

|URL|headers|methods|
|--|--|--|
|/api/v1.0/mybooks/|"token":string|POST|

**URL:Params:None**

**POST Data:**

```
{
    "username":string
}
```
**RETURN Data:**
```
{
    "lend" : [{
               "no":string,
	       "bookname":string,
	       "return_time"
           }
          ]
}

**Status code:**

```
200 OK

401 confirm failed
```
***

## 1.xls 文件约定

|序号|A|B|C|...|
|--|--|--|--|--|
|1|组别|编号|书名|..|
|2|1|T0001|TEST|..|
|..|..|..|..|..|

如上，文件格式，其余信息不全的书籍放在除前三列的位置


第一行**不能**写书籍信息，正式的书籍信息从第二行开始

如上，文件名必须是1.xls
