# `Dart` 实现

`Dart` 采用的 `Knuth-Durstenfeld Shuffle` 算法予以实现:

```dart
void shuffle(List elements, [int start = 0, int? end, Random? random]) {
  random ??= Random();
  end ??= elements.length;
  var length = end - start;
  while (length > 1) {
    var pos = random.nextInt(length);
    length--;
    var tmp1 = elements[start + pos];
    elements[start + pos] = elements[start + length];
    elements[start + length] = tmp1;
  }
}
```

* [源码](https://github.com/dart-lang/sdk/blob/df895a8a573c159935bfef235221037eec467513/sdk/lib/collection/list.dart#L363-L375)

# `JavaScript` 实现

```javascript
// 1.
const shuffle = (arr) => {
	return arr.sort(() => 0.5 - Math.random());
};

// 2.
const shuffle = (arr) => {
	const result = [];
	let random;
	while(arr.length) {
		random = Math.floor(Math.random() * arr.length);
		result.push(arr[random]);
		arr.splice(random, 1);
	}
	return result;
};
```


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
	while(length > 1) {
		pos = Math.floor(Math.random() * length);
		length--;
		// swap
		[arr[start + pos], arr[start + length]] = [arr[start + length], arr[start + pos]];
	}
	return arr;
};
```

## `Lodash` 实现

> [!tip]
> shuffle -> arrayShuffle -> shuffleSelf

```javascript
// 1. shuffle
function shuffle(collection) {
	var func = isArray(collection) ? arrayShuffle : baseShuffle;
	return func(collection);
}

// 2. arrayShuffle
function arrayShuffle(array) {
	return shuffleSelf(copyArray(array));
}

// 3. shuffleSelf
function shuffleSelf(array, size) {

	var index = -1,
		length = array.length,
		lastIndex = length - 1;

	size = size === undefined ? length : size;
	while (++index < size) {
		var rand = baseRandom(index, lastIndex),
			value = array[rand];

		array[rand] = array[index];
		array[index] = value;
	}
	array.length = size;
	return array;
}
```

* [shuffle](https://github.com/lodash/lodash/blob/ddfd9b11a0126db2302cb70ec9973b66baec0975/lodash.js#L9816-L9819)
* [arrayShuffle](https://github.com/lodash/lodash/blob/ddfd9b11a0126db2302cb70ec9973b66baec0975/lodash.js#L2441-L2443)
* [shuffleSelf](https://github.com/lodash/lodash/blob/ddfd9b11a0126db2302cb70ec9973b66baec0975/lodash.js#L6711-L6726)

# Reference

* [洗牌算法 (shuffle) 的 js 实现](https://github.com/ccforward/cc/issues/44)
* [Shuffle an array - JAVASCRIPT.INFO](https://javascript.info/task/shuffle)
* [Fisher-Yates shuffle - Wikipedia](https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle)
* [Fisher–Yates Shuffle Visualization](https://bost.ocks.org/mike/shuffle/)