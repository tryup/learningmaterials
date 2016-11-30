
###Chapter2
1. 描述下列表达式求值之后的结果：
```lisp
(a) (+ (- 5 1) (+ 3 7))
lisp使用前缀表达式，且从左往右依次计算表达式。
计算过程如下:
 step1 计算(- 5 1) ==> 表达式5返回5,表达式1返回1 后调用`-`函数。结果是4
 step2 计算(+ 3 7) ==>表达式3返回3，表达式7返回7 后调用`+`函数。记过是10.
 step3 计算(+ 4 10) 最终结果是14

(b) (list 1 (+ 2 3))
list函数是创建一个列表： (1 5)

(c) (if (listp 1) (+ 1 2) (+ 3 4))
注意第二章中的if宏的具体定义. "if cond then else"。其次注意 listp函数用来判断参数是否是一个列表。
由于1不是列表所以执行 (+ 3 4) 结果是7。
(d) (list (and (listp 3) t) (+ 1 2))
注意and宏的意义，依次执行表达式，如果遇到为假的则返回假，反之则返回最后一个表达式的值。
(and (listp 3) t) 返回nil, (+ 1 2 )返回3 故最后结果是 (nil 3)。
```
2. 给出 3 种不同表示 (a b c) 的 cons 表达式 。

```lisp
(cons 'a '(b c))
(cons 'a (cons 'b '(c)))  #如果是(cons 'a cons( 'b 'c))是什么结果？需要了解cons函数的定义
(cons 'a (cons 'b (cons 'c nil)))
```

3. 使用 car 与 cdr 来定义一个函数，返回一个列表的第四个元素。

4. 定义一个函数，接受两个实参，返回两者当中较大的那个。

5. 这些函数做了什么？
```lisp
(a) (defun enigma (x)
      (and (not (null x))
           (or (null (car x))
               (enigma (cdr x)))))

(b) (defun mystery (x y)
      (if (null y)
          nil
          (if (eql (car y) x)
              0
              (let ((z (mystery x (cdr y))))
                (and z (+ z 1))))))
```
6. 下列表达式， x 该是什么，才会得到相同的结果？
```lisp
(a) > (car (x (cdr '(a (b c) d))))
    B
(b) > (x 13 (/ 1 0))
    13
(c) > (x #'list 1 nil)
    (1)
```
7. 只使用本章所介绍的操作符，定义一个函数，它接受一个列表作为实参，如果有一个元素是列表时，就返回真。
8. 给出函数的迭代与递归版本：
   接受一个正整数，并打印出数字数量的点。
   接受一个列表，并返回 a 在列表里所出现的次数。
9. 一位朋友想写一个函数，返回列表里所有非 nil 元素的和。他写了此函数的两个版本，但两个都不能工作。请解释每一个的错误在哪里，并给出正确的版本。
```lisp
(a) (defun summit (lst)
      (remove nil lst)
      (apply #'+ lst))

(b) (defun summit (lst)
      (let ((x (car lst)))
        (if (null x)
            (summit (cdr lst))
            (+ x (summit (cdr lst))))))
```
