## 說明

1. 答案直接寫在這個 `mid-term.md` 裡，並使用 Markdown 語法撰寫。
1. 題目總共分 Ruby、Rails 以及 Git 三大主題，請在每個主題完成時進行 Commit。
1. 完成後，請發送 PR 至 `mid-term` 分支。
1. 也就是說，你的 PR 應該只會有三或四次的 Commit。

## Ruby 題目 (50 分)

1. (10 分) 請完成本題實作內容

```ruby
class Cat
  # 請完成實作
  def initialize(n)
    @n = n
  end
  
  def name
    "#{@n}"
  end
end

kitty = Cat.new("kitty")
puts kitty.name  # 在畫面上印出 kitty 字樣
```

2. (5 分) 假設有個 Hash：

```ruby
profile = {name: "kk", age: 18}
```

當執行這行程式：

```ruby
p profile["name"]
```

會得到什麼結果? 為什麼?
- 會得到nil，因為在Ruby裡要從Hash讀取key的值時，是要Symbol(eg. profile[:name])而不是用雙引號，否則不會讀到任何東西。

3. (5 分) 如果要在 1 到 100 的數字當中，任意取出 5 個不重複的亂數，你會怎麼做？
- ```puts [*1..100].sample(5) ```

4. (10 分)
```ruby
class Bank
  def transfer(amount)
    # ...
  end
end

Bank.transfer(10)
```

上面這段程式碼執行後會發生什麼事？為什麼？如果有錯誤又該如何修正？
- 會顯示錯誤：undefined method `transfer' for Bank:Class (NoMethodError) <br>
  因為要使用類別方法時，要用new方法去呼叫，且要初始化(initialize)才能傳參數。<br>
  修正結果如下：<br>
  ```ruby
  class Bank
    def initialize (amount)
      @amount = amount
    end
    def transfer
      # ...
    end
  end

  correct = Bank.new(10)
  puts correct.transfer
  ```

5. (10 分) 請問以下方法：

```ruby
link_to "刪除", products_path(product), method: :delete, class: "btn btn-default"
```

`link_to` 方法共有幾個參數？為什麼？
- 總共有<b>三個參數</b>，第一個參數為 "刪除" ，第二個為 products_path(product)，第三個為 method: :delete, class: "btn btn-default"，第三個本來
  是一個Hash→{method: :delete, class: "btn btn-default"}，但因為Ruby的簡潔寫法，去掉了大括號，所以它們原本代表一個參數。

6. (10 分) 在 Ruby 裡面常會看到冒號的寫法，例如：

有的冒號靠右邊：

```ruby
class Store
  has_many :products
end
```

有的冒號靠左邊：

```ruby
link_to "檢視", books_path(book), class: "btn btn-default"
```

或是兩邊都有：

```ruby
user_profile = {name: "kk", age: 18, blood_type: :b_negative}
```

請問，這三種寫法分別代表什麼意思呢？
- 冒號在左邊的(:product)為Symbol(帶有名字的物件)
- 冒號在右邊的(class:)類似路徑的概念，eg.class方法裡的btn樣式
- 兩邊都有冒號的(blood_type: :b_negative)為namespace，eg.找尋blood_type的namespace然後回傳b_negative裡的參數

## Rails 題目 (30 分)

1. (10 分) 請簡述 `bundle install` 指令的用途。
- 會根據 Gemfile 裡頭的設定自動下載和安裝 gem ，並能幫忙解決相依問題

2. (10 分) 請說明 `rails db:migrate` 這個指令的用途是什麼？
- 執行Migration動作

3. (10 分) 假設某個 Controller 的程式碼如下：

```ruby
class BooksController < ApplicationController
  def index
    @books = Book.all
  end

  def update
    @book = Book.find_by(id: params[:id])
    @book.update(price: 100)
    redirect_to books_path, notice: "資料更新成功"
  end
end
```

請問：
- 第 3 行的 `@books` 前面的那個 `@` 是什麼意思？如果把 `@` 拿掉會發生什麼事？
- 第 7 行以及第 8 行的 `@book`，如果把 `@` 拿掉會發生什麼事？為什麼？
  - @ 為instance variable，如果拿掉@，books就會變成local variable，index的view會讀取不到Book.All <br>
  - update會無法執行，因為book變成local variable，因為值無法傳到view

## Git 題目 (20 分)

1. (10 分) 在你想像中的分支(branch)，是個什麼樣子的東西?
- 類似樹狀圖的結構，每個分支都會有不同名稱，但是那個分支名稱像是貼標籤那樣可以撕下來，貼在想要的節點位置

2. (5 分) 空的資料夾無法被加入 Git 版控，但如果就是想讓這個資料夾留下來，你會怎麼處理?
- 將資料夾加入.keep檔案

3. (5 分) 如果有些檔案，像是 `/config/database.yml` 之類比較機密的檔案，不想放在 Git 裡面，你會怎麼做？
- 將檔案名稱加入到忽略檔(.gitignore)

## 額外加分題 (20 分)

在你之前的作業中曾寫到：

```ruby
def odd_number_calculator(n)
  #原方法
  sum = 0
  1.upto(n) do |i|
    if(i % 2 != 0)
      sum += i
    end

  #reduce
  [*1..n].select(&:odd?).reduce(:+)

  end

  return sum
end

puts odd_number_calculator(100) # 得到 2500
```

上述程式中，第 10 行的 `select` 方法用了 `&:odd?` 以及 `reduce` 後面接了 `:+` 的意思是什麼呢?

