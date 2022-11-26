## Code

const x = 5; //it's a prime number
const isPrime = (x) => {
let sqrtnum = Math.floor(Math.sqrt(x));
let prime = true
for(let i = 2; i < sqrtnum + 1; i++){
if(x % i === 0){
prime = false;
return false
};
};
return true;
}

const nextPrime = (x) => {
while(!isPrime(++x)){
};
return x;
};

const primeNum = isPrime(x)

if(primeNum){
console.log(`The ${x} is a prime number.`)
const y = nextPrime(x)
const difference = y - x
console.log(`The difference between ${y} and ${x} is ${difference}.`)
}
else{
console.log(`The ${x} is not a prime number.`)

}

## Output

The 5 is a prime number.
The difference between 7 and 5 is 2.
