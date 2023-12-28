### 💡 Title - Solution:

```
const titleName = 'Financial Analysis';
const spaceLine = '-'.repeat(16);

console.log(`${titleName} \n${spaceLine} `);

```
### 1️⃣ Total Number of Months - Solution:

```

let allMonths = finances.map(entry => entry[0].split('-')[0]);
let totalMonths = allMonths.length;

console.log(`Total number of months: ${totalMonths}`);

```
### 2️⃣ Net Total Amount of Profit/Losses - Solution:

```
const netTotal = finances.reduce((total, entry) => total + entry[1], 0);

let formattedNetTotal = new Intl.NumberFormat('en-US', {
  style: 'currency',
  currency: 'USD',
  minimumFractionDigits: 0,
  maximumFractionDigits: 0
}).format(netTotal).replace(/,/g, '');

console.log(`Total: ${formattedNetTotal}`);

```
### 3️⃣ Average Changes in Profit/Losses - Solution:

```
let totalChange = 0;

for (let i = 1; i < finances.length; i++){totalChange += finances[i][1] - finances[i - 1][1];}

const averageChange = (totalChange / (finances.length - 1)).toFixed(2);

console.log(`Average Change: ${averageChange}`);

```
### 4️⃣ Greatest Increase in Profit/Losses - Solution:

```
const searchGreatestIncrease = finances => {
  const [date, increaseDifference] = finances.slice(1).reduce(
    ([maxDate, maxDiff], [currDate, currAmount], i) => 
      (currAmount - finances[i][1] > maxDiff) ? 
      [currDate, currAmount - finances[i][1]] : [maxDate, maxDiff],
    ['', 0]
  );
  return { date, increaseDifference };
};

const { date, increaseDifference } = searchGreatestIncrease(finances);

let increaseFormat = new Intl.NumberFormat('en-US', {
  style: 'currency',
  currency: 'USD',
  minimumFractionDigits: 0,
  maximumFractionDigits: 0
}).format(increaseDifference).replace(/,/g, '');

console.log(`Greatest Increase in Profit/Losses: ${date} (${increaseFormat})`);

```
### 5️⃣ Greatest Decrease in Profit/Losses - Solution:

```
const searchGreatestDecrease = finances => {
  const greatestDecrease = finances.slice(1).reduce((result, [currentDate, currentAmount], i) => {
    const previousAmount = finances[i][1];
    const decreaseDifference = currentAmount - previousAmount;

    if (decreaseDifference < result.decreaseDifference) {
      result.date = currentDate;
      result.decreaseDifference = decreaseDifference;
    }

    return result;
  }, { date: '', decreaseDifference: Infinity });

  return greatestDecrease;
};

const result = searchGreatestDecrease(finances);

let decreaseFormat = new Intl.NumberFormat('en-US', {
  style: 'currency',
  currency: 'USD',
  minimumFractionDigits: 0,
  maximumFractionDigits: 0
}).format(result.decreaseDifference).replace(/,/g, '');

console.log(`Greatest Decrease in Profit/Losses: ${result.date} (${decreaseFormat})`);

```
