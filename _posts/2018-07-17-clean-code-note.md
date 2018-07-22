---
layout: post
title: Clean Code 筆記
categories: Note
tags: CleanCode Note
comments: true
---

A Handbook of Agile Software Craftsmanship by *Robert C. Martin*.

## Chapter 1: Clean Code

> You are reading this book for two reasons. First, you are a programmer. Second, you want
to be a better programmer. Good. We need better programmers.

*--MORE--*

- 雜亂程式碼的代價 The Total Cost of Owning a Mess

<center>
![](ProductivityVStime.jpg)
</center>

- 最根本的難題 The Primal Conundrum

	(The only way to go fast — is to keep the code as clean as possible at all times.)

- What Is Clean Code?

	- Elegant		
	- Clean code does one thing well.
	- Clean code is focused. 
		- Each function, each class, each module exposes a single-minded attitude that remains entirely undistracted, and unpolluted, by the surrounding details.

Beck’s rules of simple code. In priority order, simple code:

- 可通過所有測試 Runs all the tests
- 程式碼沒有重複 Contains no duplication
- 能表達系統設計構思 Expresses all the design ideas that are in the system
- 將類別, 方法, 函式等數量最小化 Minimizes the number of entities such as classes,
methods, functions, and the like.

## Chapter 2: Meaningful Names

- Use Intention-Revealing Names
- 避免誤導 Avoid Disinformation
- 有意義的區別 Make Meaningful Distinctions
- 能唸出來的名稱 Use Pronounceable Names
- 類別和方法的命名 Class and Methond Names

### Use Intention-Revealing Names

The name **y** and **d** reveals nothing.
  
	int y; // 年份
	int d; // 天數

Choosing names that reveal intent can make it much easier to understand and change
code.

	int elapsedTimeInYears;
	int elapsedTimeInDays;

### Avoid Disinformation

A truly awful example of disinformative names would be the use of lower-case L or
uppercase O as variable names, especially in combination. 

    int a = l;
    if ( O == l ) 
		a = O1;
    else 
		l = 01;

### Make Meaningful Distinctions

數字序列命名法 Number-series naming (a1, a2, .. aN) is the opposite of intentional naming. 

    public static void copyChars(char a1[], char a2[]) {
		for (int i = 0; i < a1.length; i++) {
			a2[i] = a1[i];
		}
    }

This function reads much better when **source** (a1) and **destination** (a2) are used for the argument
names.

- 避免使用讀者沒有辦法分辨的字

	如:你有一個 Product class, 又有另一個 ProductInfo or ProductData class, 而 Info 和 Data 是不可區分的無意義單字如 a, an, and the.

> 無意義的字是另一種沒有意義的區別 Noise words are another meaningless distinction. 


- 每個概念使用同一種字, 並堅持持續使用他

	避免在某些方法使用 get, 其他方法中又混用 fetch, retrieve.

- 避免雙關語 Don’t Pun

	不要使用同一字代表兩種不同的目的, 如 add. 使用 insert 或者是 append 易於理解.

### Use Pronounceable Names

    private Date genymdhms; 
    private Date modymdhms;

What is the significance of the value **genymdhms**?
    
    private Date generationTimestamp;    // 產生時戳
    private Date modificationTimestamp;; // 修改時戳

Make your names pronounceable.

### Class and Methond Names
 
- **Classes** 和  **objects** 應使用 名詞 或 名詞片語 來命名.

	如: Customer, WikiPage, Account, and AddressParser, 
	但避免使用 Manager, Processor, Data, 或 Info 來命名類別(Class)

- **Methods** 應使用 動詞 或 動詞片語 來命名.

	如: postPayment, deletePage, or save.


	Accessors, mutators, and predicates should be named for their value and prefixed with **get**,
**set**, and **is** according to the javabean standard.


## Chapter 3: Functions

### Functions 的首要準則 - Small

- The first rule of functions is that they should be **small**. 
- The second rule of functions is that they should be smaller than that.
- Do One Thing.

> FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL.
THEY SHOULD DO IT ONLY.

### Function Arguments

最理想的參數數量是 0, 除非有特殊理由, 否則不應該超過3個參數

> Master programmers think of systems as stories to be told rather than programs to
be written.

程式設計大師說故事而非寫程式

## Chapter 4: Comments

> “Don’t comment bad code—rewrite it.” — Brian W. Kernighan and P. J. Plaugher1


### Explain Yourself in Code

好的程式碼不需要註解, 適當的註解是用來彌補我們程式碼表達意圖失敗

- The proper use of comments is to compensate for our failure to express ourself in code.

#### 規定型註解 Mandated Comments

若每個函式都有一個 Javadoc, 只會混淆程式碼使得更加凌亂

	/**
	 * @param title The title of the CD
	 * @param author The author of the CD
	 * @param tracks The number of tracks on the CD
	 */
	public void addCD(String title, String author,
		int tracks, int durationInMinutes) {
		CD cd = new CD();
		cd.title = title;
		cd.author = author;
		cd.tracks = tracks;
	}
#### 日誌型註解 Journal Comments

以前因缺乏管控系統才需要日誌維護, 現在不應該使用這樣的註解

	/**
	 *	27-Aug-2002 : Fixed bug in addMonths() method, thanks to N???levka Petr (DG);
	 *	03-Oct-2002 : Fixed errors reported by Checkstyle (DG);
	 *	13-Mar-2003 : Implemented Serializable (DG);
	 *	29-May-2003 : Fixed bug in addMonths method (DG);
	 *	04-Sep-2003 : Implemented Comparable. Updated the isInRange javadocs (DG);
	 */

#### 干擾型註解 Noise Comments
多餘的註解 - 表達很明顯的事實, 又沒有提供任何新資訊
	
	/**
	 * Default constructor.
	 */
	private int dayOfMonth;

And then there’s this paragon of redundancy:

	/**
	 * Returns the day of the month.
	 *
	 * @return the day of the month.
	 */
	public int getDayOfMonth() {
		return dayOfMonth;
	}

#### 出處&署名 Attributions and Bylines

此類註解隨時間會變得越來越不準確, 透過管控系統會是一種比較好的選擇

	/* Added by Coie */

#### 被註解起來的程式碼 Commented-Out Code

此類註解讓人看來會沒有勇氣刪除它, 或許會有留著的理由但又或者是忘記清理的程式碼, 看了hen討m !

	InputStreamResponse response = new InputStreamResponse();
	response.setBody(formatter.getResultStream(), formatter.getByteCount());
	// InputStream resultsStream = formatter.getResultStream();
	// StreamReader reader = new StreamReader(resultsStream);
	// response.setContent(reader.read(formatter.getByteCount()));

## Chapter 5: Formatting

## Chapter 6: Objects and Data Structures

### The Law of Demeter

> A module should not know about the innards of the objects it manipulates.


## Chapter 7: Error Handling

### Use Exceptions Rather Than Return Codes

	public class DeviceController {
		...
		public void sendShutDown() {
			DeviceHandle handle = getHandle(DEV1);
			// Check the state of the device
			if (handle != DeviceHandle.INVALID) {
				// Save the device status to the record field
				retrieveDeviceRecord(handle);

				// If not suspended, shut down
				if (record.getStatus() != DEVICE_SUSPENDED) {
					pauseDevice(handle);
					clearDeviceWorkQueue(handle);
					closeDevice(handle);
				} else {
					logger.log("Device suspended. Unable to shut down");
				}
			} else {
				logger.log("Invalid handle for: " + DEV1.toString());
			}
		}
		...
	}

After we’ve chosen to throw exceptions in methods that can detect errors. (使用例外事件)

	public class DeviceController {
		...
		public void sendShutDown() {
			try {
				tryToShutDown();
			} catch (DeviceShutDownError e) {
				logger.log(e);
			}
		}
	
		private void tryToShutDown() throws DeviceShutDownError {
			DeviceHandle handle = getHandle(DEV1);
			DeviceRecord record = retrieveDeviceRecord(handle);
			pauseDevice(handle);
			clearDeviceWorkQueue(handle);
			closeDevice(handle);
		}

		private DeviceHandle getHandle(DeviceID id) {
			...
			throw new DeviceShutDownError("Invalid handle for: " + id.toString());
			...
		}

		...
	}

### Deﬁne Exception Classes in Terms of a Caller’s Needs

比較不好的例外分類 (包含所有可能拋出的例外事件, 許多重複程式碼):

	ACMEPort port = new ACMEPort(12);
	try {      
		port.open();    
		} catch (DeviceResponseException e) {      
			reportPortError(e);      
			logger.log("Device response exception", e);    
		} catch (ATM1212UnlockedException e) {      
			reportPortError(e);      
			logger.log("Unlock exception", e);    
		} catch (GMXError e) {      
			reportPortError(e);      
			logger.log("Device response exception");    
		} finally {      
			…   
		}
	}

By wrapping the API, 確保傳回共用的例外型態, 即可大幅簡化程式.

	LocalPort port = new LocalPort(12);
	try {
		port.open();
	} catch (PortDeviceFailure e) {
		reportError(e);
		logger.log(e.getMessage(), e);
	} finally {
		…
	}

透過 LocalPort wrapper (包裹), 可以幫助 fetch ACMEPort Class 所拋出的例外事件:
	
	public class LocalPort {
		private ACMEPort innerPort;

		public LocalPort(int portNumber) {
			innerPort = new ACMEPort(portNumber);
		}

		public void open() {
			try {
				innerPort.open();
			} catch (DeviceResponseException e) {
				throw new PortDeviceFailure(e);
			} catch (ATM1212UnlockedException e) {
				throw new PortDeviceFailure(e);
			} catch (GMXError e) {
				throw new PortDeviceFailure(e);
			}
		}
		…
	}

包裹第三方API是非常好的實作技巧, 可減少對API的依賴

### 不要回傳空值 Don’t Return Null

	public void registerItem(Item item) {
		if (item != null) {
			ItemRegistry registry = peristentStore.getItemRegistry(); //如果 peristentStore 是空值???
			if (registry != null) {
				Item existing = registry.getItem(item.getID());
				if (existing.getBillingPeriod().hasRetailOwner()) {
					existing.register(item);
				}
			}
		}
	}


In many cases, special case objects are an easy remedy. Imagine that you have code
like this:

	List<Employee> employees = getEmployees();
	if (employees != null) {
		for(Employee e : employees) {
			totalPay += e.getPay();
		}
	}

將 getEmployees 修改為回傳 empty list 而非回傳 null (空值):

	List<Employee> employees = getEmployees();
	for(Employee e : employees) {
		totalPay += e.getPay();
	}

在 Java 可以利用 Collections.emptyList() 回傳一個預先定義的 immutable list (不可變串列):

	public List<Employee> getEmployees() {
	if( .. there are no employees .. )
		return Collections.emptyList();
	}

就可以降低 NullPointerExceptions 發生機率, 使得程式碼更乾淨！

### 不要傳遞空值 Don’t Pass Null

> Returning null from methods is bad, but passing null into methods is worse.

除非使用的 API 會預期你可能傳空值, 否則應避免傳遞空值

	public class MetricsCalculator
	{
		public double xProjection(Point p1, Point p2) {
			return (p2.x – p1.x) * 1.5;
		}
		…
	}

What happens when someone passes **null** as an argument? **NullPointerExceptions !!**

There is another alternative. We could use a set of assertions:

	public class MetricsCalculator
	{
		public double xProjection(Point p1, Point p2) {
			assert p1 != null : "p1 should not be null";
			assert p2 != null : "p2 should not be null";
			return (p2.x – p1.x) * 1.5;
		}
	}

It’s good documentation, but it doesn’t solve the problem. If someone passes null, we’ll
still have a runtime error. 

## Chapter 8: Boundaries

### Using Third-Party Code

第三方軟體通常具有廣泛的適用性, 但另一方面使用者希望介面能夠專注於他們的需求

Let’s look at java.util.Map as an example. 

例如: 應用程式中需要一個 Sensors 的 Map, 則我們可能會看到:

	Map sensors = new HashMap();

當其他程式需要存取 Sensors 時, 你會看到

	Sensor s = (Sensor)sensors.get(sensorId );

從 Map 中取得物件再將他轉型, 這樣的作法並不是 clean code.

使用泛型 (generics) 可以改善程式碼的可讀性

	Map<Sensor> sensors = new HashMap<Sensor>();
	Sensor s = sensors.get(sensorId );

## Chapter 9: Unit Tests

寫程式之前, 必須先寫好單元測試

### The Three Laws of TDD (Test Driven Development)

1. First Law You may not write production code until you have written a failing unit test.

2. Second Law You may not write more of a unit test than is sufficient to fail, and not compiling is failing.

3. Third Law You may not write more production code than is sufficient to pass the currently
failing test.


## Chapter 10: Classes
## Chapter 11: Systems
## Chapter 12: Emergence
## Chapter 13: Concurrency
## Chapter 14: Successive Refinement
## Chapter 15: JUnit Internals
## Chapter 16: Refactoring SerialDate
## Chapter 17: Smells and Heuristics.

### Comments

- C1: 不適當的資訊 Inappropriate Information
- C2: 廢棄的註解 Obsolete Comment
- C3: 多餘的註解 Redundant Comment
- C4: 寫得不好的註解 Poorly Written Comment
- C5: 被註解掉的程式碼 Commented-Out Code


### Environment

- E1: Build Requires More Than One Step
- E2: Tests Require More Than One Step

### Functions

- F1: Too Many Arguments
- F2: Output Arguments
- F3: Flag Arguments
- F4: Dead Function


### General

- G1: Multiple Languages in One Source File
- G2: Obvious Behavior Is Unimplemented
- G3: Incorrect Behavior at the Boundaries
- G4: Overridden Safeties
- G5: Duplication
- G6: Code at Wrong Level of Abstraction
- G7: Base Classes Depending on Their Derivatives
- G8: Too Much Information
- G9: Dead Code
- G10: Vertical Separation
- G11: Inconsistency
- G12: Clutter
- G13: Artificial Coupling
- G14: Feature Envy
- G15: Selector Arguments
- G16: Obscured Intent
- G17: Misplaced Responsibility
- G18: 不適當的靜態宣告 Inappropriate Static
- G19: 解釋性的變數 Use Explanatory Variables
- G20: Function Names Should Say What They Do
- G21: Understand the Algorithm
- G22: 實體相依 Make Logical Dependencies Physical
- G23: 善用多型 Prefer Polymorphism to If/Else or Switch/Case
- G24: 標準慣例 Follow Standard Conventions
- G25: Replace Magic Numbers with Named Constants
- G26: Be Precise
- G27: 結構勝於常規 Structure over Convention
- G28: 封裝條件判斷 Encapsulate Conditionals

	For example:
	
		if (shouldBeDeleted(timer))
	
	is preferable to
	
		if (timer.hasExpired() && !timer.isRecurrent())

- G29: 避免否定判斷 Avoid Negative Conditionals

	For example:

		if (buffer.shouldCompact())

	is preferable to

		if (!buffer.shouldNotCompact())

- G30: Functions Should Do One Thing
- G31: Hidden Temporal Couplings
- G32: Don’t Be Arbitrary
- G33: Encapsulate Boundary Conditions
- G34: Functions Should Descend Only One Level of Abstraction
- G35: Keep Configurable Data at High Levels
- G36: Avoid Transitive Navigation

### Java

- J1: Avoid Long Import Lists by Using Wildcards
- J2: Don’t Inherit Constants
- J3: Constants versus Enums

### Names

- N1: 具有描述的名稱 Choose Descriptive Names
- N2: Choose Names at the Appropriate Level of Abstraction
- N3: 使用標準命名 Use Standard Nomenclature Where Possible
- N4: 非模稜兩可的名稱 Unambiguous Names
- N5: Use Long Names for Long Scopes
- N6: 避免編碼 Avoid Encodings
- N7: 命名應描述可能的副作用 Names Should Describe Side-Effects

### Tests

- T1: 不足夠的測試 Insufficient Tests
- T2: Use a Coverage Tool!
- T3: 不要跳過簡單的測試 Don’t Skip Trivial Tests
- T4: 被忽略的測試是模稜兩可的疑問 An Ignored Test Is a Question about an Ambiguity
- T5: Test Boundary Conditions
- T6: 在程式錯誤附近進行詳盡的測試 Exhaustively Test Near Bugs
- T7: Patterns of Failure Are Revealing
- T8: Test Coverage Patterns Can Be Revealing
- T9: Tests Should Be Fast