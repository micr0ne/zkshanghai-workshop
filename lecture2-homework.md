# 第2课 课后作业

## 转换为bit位 Num2Bits
pragma circom 2.1.4;

template nBits(n){
    signal input in;
    signal output out[n];
    for(var i = 0; i < n; i++){
    out[i] <-- in>>i & 1;
    out[i]*(out[i] - 1) === 0;
}

}

component main  = nBits(254);

/* INPUT = {
"in": "77"
} */
## ISzero
pragma circom 2.1.4;

template IsZero(){
    signal input in;
    signal output out;

signal tem;
tem <-- in==0? 0 : 1/in;
out <== -in*tem + 1;
in*out === 0;

}

component main  = IsZero();

/* INPUT = {
    "in": "77"
} */
IsEqual
pragma circom 2.1.4;


template IsZero(){
    signal input in;
    signal output out;

signal tem;
tem <-- in==0? 0 : 1/in;
out <== -in*tem + 1;
in*out === 0;

}


template IsEqual(){

    signal input in[2];
    signal output out;

    component iszero = IsZero();
    iszero.in <== in[0] - in[1];
    out <== iszero.out;
log("s",out);
}

component main  = IsEqual();

/* INPUT = {
    "in": ["2","2"]
    
} */


## 选择器 Selector
pragma circom 2.1.4;

template IsZero(){
    signal input in;
    signal output out;

signal tem;
tem <-- in==0? 0 : 1/in;
out <== -in*tem + 1;
in*out === 0;

}
template  CalculateToal(n) {
    signal input in[n];
    signal output out;

    signal sum[n];

    sum[0] <== in[0];
    for(var i = 1; i < n; i++) 
    {
        sum[i] <== sum[i-1] + in[i];
    }

    out <== sum[n-1];
}

template IsEqual(){

    signal input in[2];
    signal output out;

    component iszero = IsZero();
    iszero.in <== in[0] - in[1];
    out <== iszero.out;

}


template  Selector(choices){
signal input in[choices];
signal input index;
signal output out;
//计算数组总数
component Calcu = CalculateToal(choices);
//构建一个判断组件
component  jug[choices];

//遍历数组每个数是否与index 相等
for ( var i = 0; i < choices; i++) {
    jug[i] = IsEqual();
    jug[i].in[0] <== i;
    jug[i].in[1] <== index;

    Calcu.in[i] <== jug[i].out * in[i];

}

    out <== Calcu.out;

}

component main = Selector(5);

/* INPUT = {
    "in":["1","2","3","4","5"],
    "index":"3"
}
*/

## 判负
pragma circom 2.1.4;

template Sign(){
    signal input in[254];
    signal output out;
    component comp = CompConstant(10944121435919637611123202872628637544274182200208017171849102093287904247808)
    for(var i = 0; i < 254; i++){
      comp.in[i] <== in[i];
  }
    out <== comp.out;
}

template IsNegative(n){
    signal input in;
    signal output out;
    component sign = Sign();

    for(var i = 0; i < n; i++){
      sign.in[i] <-- in>>i & 1;
      sign.in[i]*(sign.in[i] - 1) === 0;
  }
    out <== sign.out;
}

component main  = IsNegative(254);



/*INPUT = {
"in":"10"
}
*/




LessThan
pragma circom 2.1.4;

// template  Lessthan(n){
//     assert(n<=252);
//     signal input in[2];
//     signal output out;
//     component  n2b = Num2Bits(n);
//     n2b.in <== in[0] + (1<<n) - in[1];

//     out <== 1 - n2b.out[n-1];
// }

template nBits(n){
    signal input in;
    signal output out[n];
    for(var i = 0; i < n; i++){
    out[i] <-- in>>i & 1;
    out[i]*(out[i] - 1) === 0;
}

}

template LessEqthan(n)
{
     assert(n<=252);
    signal input in[2];
    signal output out;
    signal inv;
    inv <== in[1]+1;
    component  n2b = nBits(n+1);
    n2b.in <== in[0] + (1<<n) - inv;


    out <== 1 - n2b.out[n];
}


// template  Greaterthan(n){
//     assert(n<=252);
//     signal input in[2];
//     signal output out;
//     component  n2b = nBits(n);
//     n2b.in <== in[1] + (1<<n) - in[0];

//     out <== 1 - n2b.out[n-1];
// }

template  GreaterEqthan(n){
    assert(n<=252);
    signal input in[2];
    signal output out;
    signal inv;
    inv <== in[1]+1;
    component  n2b = nBits(n);

    n2b.in <== inv + (1<<n) - in[0];

    out <== 1 - n2b.out[n-1];
}

component main = LessEqthan(252);

/* INPUT = {
    "in": ["6","5"]
} */
## 整除
整除
pragma circom 2.1.4;

include "circomlib/comparators.circom";
include "circomlib/sign.circom";

template IsNegative(n){
    signal input in;
    signal output out;
    component si = Sign();

    for(var i = 0; i < n; i++){
      si.in[i] <-- (in>>i) & 1;
      si.in[i]*(si.in[i] - 1) === 0;
        }
    out <== si.sign;
}

template exact_divisor(divisor_bits){
    signal input dividend;
    signal input divisor;
    signal output remainder;
    signal output quotient;
    component is_neg = IsNegative(254);
    is_neg.in <== dividend;

// 如果dividend 为负，则将其转为正

    signal output is_dividend_neg;
    is_dividend_neg <== is_neg.out;
     signal output dividend_adjustment;
     dividend_adjustment <== 1 + is_dividend_neg * -2; 
     signal output abs_dividend;
     abs_dividend <== dividend * dividend_adjustment;
   
   //求负余数和正余数
     signal output raw_remaider;
     raw_remaider <-- abs_dividend % divisor;

     signal output neg_remainder;

     neg_remainder <-- divisor - raw_remaider;

    //如果dividend为正则为正余数，否者为负余数

    if(is_dividend_neg == 1 && raw_remaider != 0){
       remainder <-- neg_remainder;
     } else {
       remainder <-- raw_remaider;
     }
   
    quotient <-- (dividend - remainder) / divisor;
    dividend === quotient * divisor + remainder;

//保证余数小于除数大于等于0
    component remainderUpper = LessThan(divisor_bits);
    remainderUpper.in[0] <== remainder;
    remainderUpper.in[1] <== divisor;
    remainderUpper.out === 1;

    }

component main  = exact_divisor(252);

/* INPUT = {
    "dividend": "6",
    "divisor": "5"
} */
