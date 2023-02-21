//dictionary of all currency units and their values
let dict = {
  'PENNY': 0.01,
  'NICKEL': .05,
  'DIME': .1,
  'QUARTER': .25,
  'ONE': 1,
  'FIVE': 5,
  'TEN': 10,
  'TWENTY': 20,
  'ONE HUNDRED': 100
}

function checkCashRegister(price, cash, cid) {

  //total change for transaction
  let change = cash - price;

  //initialize return status
  let status = {
    status: '',
    change: []
  }

  //initialize CID object of change
  let changeCID = [];

  let finalCID = [];

  for (let i = cid.length - 1; i >= 0; i--){

    //Amount of change in current unit
    let changeInUnit = [cid[i][0],0];

    if (change == 0 || cid[i][1] == 0){
      finalCID.push(cid[i]);
    }

    if (change >= cid[i][1]){
      change = roundingHelper(change, cid[i][1]);
      changeInUnit[1] = cid[i][1];
      cid[i][1] = 0;
    } else {
      let currentChange = roundingHelper(change, ((change * 100) % (dict[cid[i][0]] * 100)/ 100));
      change = roundingHelper(change, currentChange);
      changeInUnit[1] = currentChange;
      cid[i][1] = roundingHelper(cid[i][1], currentChange);
    }
  
    //If there is change, add it to changeCID and finalCID
    if (changeInUnit[1] > 0){
      changeCID.push(changeInUnit);
      finalCID.push(changeInUnit);
    }
  }

  if (change > 0){
    status['status'] = 'INSUFFICIENT_FUNDS';
  } else if (cid.every(unit => unit[1] == 0)){
    status['status'] = 'CLOSED';
    status['change'] = finalCID.reverse();
  } else {
    status['status'] = 'OPEN';
    status['change'] = changeCID;
  }  
  return status;
}

function roundingHelper(num1, num2){
  return (Math.round(num1 * 100) - Math.round(num2 * 100)) / 100;
}

checkCashRegister(19.5, 20, [["PENNY", 0.5], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 0], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]])
checkCashRegister(3.26, 100, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.1], ["QUARTER", 4.25], ["ONE", 90], ["FIVE", 55], ["TEN", 20], ["TWENTY", 60], ["ONE HUNDRED", 100]]);
