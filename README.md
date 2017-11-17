## //二叉树横向遍历
```js
function TreeNode(val){
        this.val = val;
        this.left = null;
        this.right = null;
      }
      var v1 = new TreeNode(1);
      var v2 = new TreeNode(2);
      var v3 = new TreeNode(3);
      var v4 = new TreeNode(4);
      var v5 = new TreeNode(5);
      var v6 = new TreeNode(6);
      var v7 = new TreeNode(7);
      var v8 = new TreeNode(8);
      var v9 = new TreeNode(9);

      v1.left = v2;
      v1.right = v3;
      v2.left = v4;
      v2.right = v5;
      v3.left = v6;
      v3.right = v7;
      v5.left = v8;
      v5.right = v9;

      var arr = [];
     //方法1
      function walk(root, num){
        if(typeof num === 'undefined'){
          num = 0;
        }
        if(isArray(root)){
          num++;
          root.forEach(function(v){
            walk(v, num);
            console.log(num + '::', v.val);
          });
        }else{
          if(root.left !== null || root.right !== null){
            arr[num] = arr[num] || [];
            var _arr = [root.left, root.right];
            arr[num] = arr[num].concat(_arr);
            walk(_arr, num);
          }
        }
        function isArray(val){
          return Object.prototype.toString.call(val) === '[object Array]';
        }
      }

      walk(v1);
      
      //方法2
      function walk2(root){
        var index = 0;
        var arr = [];
        getNextArray(arr, root);
        printLayer(arr);
        function getNextArray(arr, v){
          console.log(index + '::', v.val);
          if(v.left){
            arr.push(v.left);
          }
          if(v.right){
            arr.push(v.right);
          }
          index === 0 && index++;
        }
        function printLayer(arr){
          var _arr = [];
          arr.forEach(function(v){
            getNextArray(_arr, v);
          });
          if(_arr.length > 0){
            index++;
            printLayer(_arr);
          }
        }
      }

      walk2(v1);
```
## 格式化数字
```js
function formatNumber(val){
        var str = val.toString().replace(/^\D/,'');
        var len = str.length;
        var num = 0;
        var arr = [];
        var pre = val < 0 ? '-' : '';
        while(len--){
          var n = +str[len];
          arr.unshift(n);
          if(++num % 3 === 0 && num >= 3 && str.length > 3 && len > 0){
            arr.unshift(',');
            num = 0 ;
          }
        }
        return pre + arr.join('');
      }

      console.log(formatNumber(-1234567890235));
```

## 快速排序
```js
function quickSort(arr){
    var len = arr.length;
    var middleIndex = Math.floor(len/2);
    var leftArr = [],rightArr = [];
    for(var i = 0; i < len; i++){
      var currentVal = arr[i];
      var middleVal = arr[middleIndex];
      if(middleIndex !== i){
        if(currentVal < middleVal){
          leftArr.push(currentVal);
        }else{
          rightArr.push(currentVal);
        }
      }
    }
    var leftResult = leftArr.length > 1 ? quickSort(leftArr) : leftArr;
    var rightResult = rightArr.length > 1 ? quickSort(rightArr) : rightArr;
    return leftResult.concat([middleVal], rightResult);
  }

  console.log(quickSort([6,4,1,7,1,2,9,8,0]));
```
