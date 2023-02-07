# `Overview`

# `Fisher-Yates Shuffle`

* [Fisher-Yates Shuffle 可视化](https://codepen.io/haoyang/pen/jMvMQq)

## `JavaScript` Implement

# `Knuth-Durstenfeld Shuffle`

* [神一样的随机算法](https://mp.weixin.qq.com/s?__biz=MzU4NTIxODYwMQ==&mid=2247484310&idx=1&sn=916f92afff6016256648cfb3c7fd83e7&chksm=fd8cacd0cafb25c670587f22524b111d74b4ddd9954070930b6ef6efb1bd8fba13d4250e57d8&token=885428195&lang=zh_CN#rd)
* [Fisher–Yates shuffle 洗牌算法](https://gaohaoyang.github.io/2016/10/16/shuffle-algorithm/)
* [Python 随机数标准库(2) – shuffle()](https://lujiaying.github.io/posts/2016/08/Python-random-2/)

## `JavaScript` Implement

```js
const shuffle = (arr, start = 0, end) => {
	if (end === undefined) {
		end = arr.length;
	}
	
	if (typeof start !== "number" || typeof end !== "number") {
		throw new Error("请检查起始和终点下标值");
	}
	
	if (end < start) {
	    // 互换
	    let temp = start;
	    start = end;
	    end = temp;
	}

	if (end === start) {
		return arr;
	}
  
	let length = end - start;
	let pos;
	while(length) {
		pos = Math.floor(Math.random() * length);
		length--;
		// swap
		[arr[start + pos], arr[start + length]] = [arr[start + length], arr[start + pos]];
	}
	return arr;
};
```

## `Dart` Implement

```dart
void shuffle(List elements, [int start = 0, int? end, Random? random]) {
  random ??= Random();
  end ??= elements.length;
  var length = end - start;
  while (length > 1) {
    var pos = random.nextInt(length);
    length--;
    var temp = elements[start + pos];
    elements[start + pos] = elements[start + length];
    elements[start + length] = temp;
  }
}
```

## `Python` Implement

[Python Knuth-Durstenfeld Shuffle Algorithm](https://gist.github.com/m00nlight/b3f7a4e4fb9ee9ddd1dd)

```python
def knuth_shuffle(items):

"""

Fisher-Yates shuffle or Knuth shuffle which name is more famous.

See <http://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle> for detail

Type : [a] -> None (shuffle inplace)

Post constrain: Should be list

Post constrain: return array of the same length of input

"""

	for i in range(len(items)):
		j = randrange(i, len(items))
		items[i], items[j] = items[j], items[i]
```

## `Rust` Implement

## `Golang` Implement

## `C` Implement

## `C++` Implement

## `Haskell` Implement