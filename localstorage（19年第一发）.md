## 概念
> HTML5中，新加入了一个localStorage特性，这个特性主要是用来作为本地存储来使用的，解决了cookie存储空间不足的问题(cookie中每条cookie的存储空间为4k)，localStorage中一般浏览器支持的是5M大小，这个在不同的浏览器中localStorage会有所不同。

## 优势与局限

### localStorage的优势

1. localStorage拓展了cookie的4K限制

2. localStorage会可以将第一次请求的数据直接存储到本地，这个相当于一个5M大小的针对于前端页面的数据库，相比于cookie可以节约带宽，但是这个却是只有在高版本的浏览器中才支持的

### localStorage的局限

1. 浏览器的大小不统一，并且在IE8以上的IE版本才支持localStorage这个属性

2. 目前所有的浏览器中都会把localStorage的值类型限定为string类型，这个在对我们日常比较常见的JSON对象类型需要一些转换

3. localStorage在浏览器的隐私模式下面是不可读取的

4. localStorage本质上是对字符串的读取，如果存储内容多的话会消耗内存空间，会导致页面变卡

5. localStorage不能被爬虫抓取到

#### ``localStorage与sessionStorage的唯一一点区别就是localStorage属于永久性存储，而sessionStorage属于当会话结束的时候，sessionStorage中的键值对会被清空``

6. ==使用上无法像cookie 一样设置过期时间。过期后无法被读取==


so github找一个封装好的，

let do it

```
// 缓存方式
const localStorage = window.localStorage;

/**
 * 设置缓存
 * @param {String} key 键
 * @param {*} value 值
 */
function setItem(key, value) {
    localStorage.setItem(key, JSON.stringify(value));
}

/**
 * 获取缓存
 * @param {String} key 键
 * @returns {*|null}
 */
 
function getItem(key) {
    const result = localStorage.getItem(key);
    if (result) {
        return JSON.parse(result);
    }
    return null;
}

/**
 * 移除缓存
 * @param key
 */
 
function removeItem(key) {
    localStorage.removeItem(key);
}

/**
 * 获取当前时间戳（毫秒）
 * @returns {number}
 */
 
function getNow() {
    return Date.parse(new Date());
}

// 缓存表前缀
const mapKey = 'lz-map-';

/**
 * localStorage 操作类
 * 支持过期时间
 */
 
class LzLocalStorage {

    /**
     * @param {String} namespace 命名空间
     */
    constructor(namespace = '') {
        // 缓存命名空间
        this.namespace = namespace;
        // 缓存表key
        this.mapKey = mapKey + this.namespace;
        // 缓存表
        this.map = getItem(this.mapKey) || {};
    }

    /**
     * 设置缓存
     * @param {String} key 键
     * @param {*} value 值
     * @param {Number} expires 过期时间（毫秒） -1不过期，
     */
    set(key, value, expires = -1) {
        const k = this.getReallyKey(key);
        const obj = {
            expires,
            time: getNow()
        };
        setItem(k, value);
        this.map[key] = obj;
        setItem(this.mapKey, this.map);
    }

    /**
     * 获取真实的缓存键
     * @param {String} key 键
     * @returns {string}
     */
    getReallyKey(key) {
        return this.namespace + "-" + key;
    }

    /**
     * 获取缓存内容
     * @param {String} key 键
     * @param {*} defaultValue 默认返回值
     * @returns {*} 若未取到则返回defaultValue
     */
    get(key, defaultValue) {
        const k = this.getReallyKey(key);
        let obj = this.map[key];
        // 缓存存在
        if (obj) {
            // 缓存无过期时间
            if (obj.expires > -1) {
                // 在缓存时间内
                if (getNow() - obj.time <= obj.expires) {
                    return getItem(k) || defaultValue;
                } else {
                    this.delete(key);
                }
            } else {
                return getItem(k) || defaultValue;
            }
        }
        return defaultValue;
    }

    /**
     * 获取命名空间下所有缓存
     * @returns {Object}
     */
     
    getAll() {
        const result = {};
        for(const i in this.map) {
            result[i] = this.get(i);
        }
        return result;
    }

    /**
     * 删除单个缓存
     * @param {String} key 键
     */
     
    delete(key) {
        const k = this.getReallyKey(key);
        delete this.map[key];
        // 重置缓存表
        setItem(this.mapKey, this.map);
        // 删除缓存
        removeItem(k);
    }

    /**
     * 删除所有命名空间缓存
     */
     
    deleteAll() {
        for(const i in this.map) {
            this.delete(i);
        }
    }
}



/**
 * @by lz
 *
 * 支持过期时间的缓存操作工具类
 *
 * 使用方法：
 * const mLzLocalStorage = new LzLocalStorage('lz');
 *
 * mLzLocalStorage.set('name', 'lz', -1);
 * mLzLocalStorage.get('name'); // 输出lz 不会过期
 *
 * mLzLocalStorage.set('name', 'lz', 3 * 1000);
 * mLzLocalStorage.get('name'); // 3秒内容可以取到lz, 3秒过后获取，取不到值，
 */
 
 
```
[github链接](https://github.com/lzuntalented/tools/blob/master/localstorage/localstorage.js)