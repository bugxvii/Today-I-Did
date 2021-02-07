tags: #algorithm #reverse-polish-notation #english 

<hr />

[[200921 중위표기식 후위표기식으로 변환하기 | 🇰🇷 한국어]]
[[200921 後置記法・逆ポーランド記法に変換 | 🇯🇵 日本語]]

## Reverse Polish Notation

An expression like `A*(B+C)` is called **infix expression**. We can represent this same expression in different ways like `ABC+*`. This form of expression where operators are on the right or post operands are called **reverse polish notation** or simply **postfix notation**.

Infix/Postfix is a very common problem that you'll encounter when you're learning about **Stack**.

Here are general steps of the algorithm.

Scan each character (operands and operators) from the infix expression and ...

1.  if it's an operand, print it.
    
    ```ruby
    if (expr[i]>='A' and expr[i]<='Z') 
        print expr[i]
    end
    ```
    
2.  if it's `(`, push it to the operator stack.
    
    ```ruby
    if (expr[i]=='(')
        op << expr[i]
    end
    ```
    
3.  if it's `)`, pop operators from the stack until it pops `(`.
    
    ```ruby
    if (expr[i]==')')
        while op.last != '('
            print op.last 
            op.pop
        end
        op.pop
    end
    ```
    
4.  if it's an operator, push it to the stack if...
    
    1.  a stack is empty,
    2.  top of the stack is `(`
    3.  scanned operator's priority is higher than the operator on top of the stack
5.  if rule #4 is not true, pop the stack until scanned operator's priority is less than or equal to the stack's top operator's priority. And then, push the scanned operator to the stack.
    
    ```ruby
    if (expr[i]=='+' or expr[i]=='-' or expr[i]=='*' or expr[i]=='/')
        ## 4번
        if (op.size==0 || op.last=='(' || 
           (priority(expr[i]) > priority(op.last)))
         op << expr[i] 
         ## 5번
        else 
            while priority(expr[i]) <= priority(op.last)
                print op.last 
                op.pop 
            end
            op << expr[i]
        end
    end
    ```
    
6.  Finally, empty out the stack.
    
    ```ruby
    op.size.times do
        print op.pop
    end
    ```
    

For example, let say we have `A*(B+C)`.

![step1](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/dd5d96fa-fa5b-4ad7-8161-7a2a5003ecd3/infix2postfix-1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210206%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210206T052833Z&X-Amz-Expires=86400&X-Amz-Signature=ce004ed6242373248250f491e350c13e7324fc04ff9172170e956ba8e2dbfb7a&X-Amz-SignedHeaders=host)

`A` is an operand. Follow the rule #1 and print it.

![step2](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7aa08ca9-13e6-463c-82c3-20bb593f1f0a/infix2postfix-2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210206%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210206T052833Z&X-Amz-Expires=86400&X-Amz-Signature=e59ba966703166d194edef5094fa74dd6b04863043f4da8fc1223e0f644ceb6c&X-Amz-SignedHeaders=host)

Push the `*` operator to the stack since it falls into the rule #4 (`stack is empty`).

And push the `(` operator to the stack based on the rule #2.

![step3](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4ecf09a9-aea3-41d6-8296-e1b4324a49ca/infix2postfix-3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210206%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210206T052833Z&X-Amz-Expires=86400&X-Amz-Signature=e3b5750417fe7e0cf5d191e0664f6bc196fae2c02eb8d3cf952795b24c8e4568&X-Amz-SignedHeaders=host)

`B` is an operand. Follow the rule #1 and print it.

For the `+` operator, it falls into the rule #4 (`top of the stack is (`), so it goes into the stack.

![step4](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e141f449-dcd4-4d34-bc05-27a351c91adc/infix2postfix-4.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210206%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210206T052833Z&X-Amz-Expires=86400&X-Amz-Signature=643b6a0a57284d454da757a8788412bcd09bc5d62872e5a8d44ae6977a4ae31c&X-Amz-SignedHeaders=host)

`C` is also an operand. Follow the rule #1 and print it.

![step5](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/25dd0591-a2a7-4e09-af80-4f6b72bb40dc/infix2postfix-5.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210206%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210206T052833Z&X-Amz-Expires=86400&X-Amz-Signature=ebe5b8a0e32e9873073ef092a8ba37d9cdaf1f70f4738e7ec00d575be613466d&X-Amz-SignedHeaders=host)

Now we encountered the `)`. Follow the rule #3 and pop the stack until it pops `(`.

We've finished scanning the expression. Finish it by popping all operators from the stack (rule #6).

![final step](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8ae1c23e-7876-4db0-af15-227ab2ce8a1e/infix2postfix-6.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210206%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210206T052833Z&X-Amz-Expires=86400&X-Amz-Signature=9201209ceadfbe1d5e0200e07adbc690b3ea61df42cf85ca2eec93d76e1d3e21&X-Amz-SignedHeaders=host)

We have finished converting an infix expression to a postfix expression.

## Entire code
- https://github.com/eubug17/ds-algo/blob/master/algorithm/stack/infix2postfix/infix2postfix.rb