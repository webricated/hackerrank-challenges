### HackerRank Javascript (Intermediate) Skills Certification Test

## Q.1 JavaScript: Parking Lot

```
'use strict';

const fs = require('fs');

process.stdin.resume();
process.stdin.setEncoding("ascii");
let inputString = "";
let currentLine = 0;

process.stdin.on("data", function (chunk) {
    inputString += chunk;
});
process.stdin.on("end", function () {
    inputString = inputString.split('\n');
    main();
});

function readLine() {
  return inputString[currentLine++];
}


class ParkingLot {
    constructor(slots) {
        this.slots = new Array(slots).fill(null);
    }

    park(carId) {
        for (let i = 0; i < this.slots.length; i++) {
            if (this.slots[i] === null) {
                this.slots[i] = carId;
                return true;
            }
        }
        return false; // Parking lot is full
    }

    getSlots() {
        return this.slots;
    }

    remove(carId) {
        for (let i = 0; i < this.slots.length; i++) {
            if (this.slots[i] === carId) {
                this.slots[i] = null;
                return true; // Car removed
            }
        }
        return false; // Car not found
    }
}


function main() {
    const ws = fs.createWriteStream(process.env.OUTPUT_PATH);
    
    const numberOfSlots = parseInt(readLine().trim());
    const parkingLotObj = new ParkingLot(numberOfSlots);
    ws.write(`Parking Lot created with number of slots as ${numberOfSlots}\n`);
    
    let numberOfOperations = parseInt(readLine().trim());
    while (numberOfOperations-- > 0) {
        const inputs = readLine().trim().split(' ');
        const operation = inputs[0];
        const carId = inputs[1];

        switch(operation) {
            case 'Park':
                if (parkingLotObj.park(carId)) {
                    ws.write(`Parking Started: ${carId}\n`);
                } else {
                    ws.write(`Parking Full: ${carId}\n`);
                }
                break;
            case 'Remove':
                if (parkingLotObj.remove(carId)) {
                    ws.write(`Car id ${carId} removed from parking\n`);
                } else {
                    ws.write(`Car: ${carId} not found\n`);
                }
                break;
            case 'GetSlots':
                const status = parkingLotObj.getSlots();
                status.forEach((obj, i) => {
                    if (obj) {
                        ws.write(`Parked at slot ${i + 1}: ${obj}\n`);
                    } else {
                        ws.write(`Slot ${i + 1} is empty\n`);
                    }
                })
                break;
            default:
                break;
        }
    }
    ws.end();
}
```

## Q.2 JavaScript: Activity List

```
'use strict';

const fs = require('fs');

process.stdin.resume();
process.stdin.setEncoding("ascii");
let inputString = "";
let currentLine = 0;

process.stdin.on("data", function (chunk) {
    inputString += chunk;
});
process.stdin.on("end", function () {
    inputString = inputString.split('\n');
    main();
});

function readLine() {
  return inputString[currentLine++];
}

// Step 1: Define the Activity constructor function
function Activity(amount) {
    this.amount = amount;
}

// Step 2: Add methods to Activity's prototype
Activity.prototype.setAmount = function(value) {
    if (value <= 0) {
        return false;
    }
    this.amount = value;
    return true;
};

Activity.prototype.getAmount = function() {
    return this.amount;
};

// Step 3: Define the Payment constructor function and inherit from Activity
function Payment(amount, receiver) {
    Activity.call(this, amount);  // Call the Activity constructor with the amount parameter
    this.receiver = receiver;     // Initialize receiver
}

// Step 4: Set up inheritance by linking Payment's prototype to Activity's prototype
Payment.prototype = Object.create(Activity.prototype);
Payment.prototype.constructor = Payment;

// Step 5: Add methods to Payment's prototype
Payment.prototype.setReceiver = function(receiver) {
    this.receiver = receiver;
};

Payment.prototype.getReceiver = function() {
    return this.receiver;
};

// Step 6: Define the Refund constructor function and inherit from Activity
function Refund(amount, sender) {
    Activity.call(this, amount);  // Call the Activity constructor with the amount parameter
    this.sender = sender;         // Initialize sender
}

// Step 7: Set up inheritance by linking Refund's prototype to Activity's prototype
Refund.prototype = Object.create(Activity.prototype);
Refund.prototype.constructor = Refund;

// Step 8: Add methods to Refund's prototype
Refund.prototype.setSender = function(sender) {
    this.sender = sender;
};

Refund.prototype.getSender = function() {
    return this.sender;
};

function main() {
    const ws = fs.createWriteStream(process.env.OUTPUT_PATH);
    
    const objectType = readLine().trim();
    
    const inputsForObjectCreation = readLine().trim().split(' ');
    const updatedAmount = parseInt(readLine().trim());
    const updatedSenderReceiver = readLine().trim();
    
    switch(objectType) {
        case 'Payment':
            const paymentObj = new Payment(parseInt(inputsForObjectCreation[0]), inputsForObjectCreation[1]);
            ws.write(`Payment object created with amount ${paymentObj.getAmount()} and receiver ${paymentObj.getReceiver()}\n`);
            if(paymentObj.setAmount(updatedAmount)) {
                ws.write(`Amount updated to ${updatedAmount}\n`);
            } else {
                ws.write(`Amount not updated\n`);
            }
            paymentObj.setReceiver(updatedSenderReceiver);
            ws.write(`Receiver updated to ${updatedSenderReceiver}\n`);
            ws.write(`Payment object details - amount is ${paymentObj.getAmount()} and receiver is ${paymentObj.getReceiver()}\n`);
            ws.write(`Payment.prototype has property setAmount: ${Payment.prototype.hasOwnProperty('setAmount')}\n`);
            ws.write(`Payment.prototype has property getAmount: ${Payment.prototype.hasOwnProperty('getAmount')}\n`);
            ws.write(`Payment.prototype has property setReceiver: ${Payment.prototype.hasOwnProperty('setReceiver')}\n`);
            ws.write(`Payment.prototype has property getReceiver: ${Payment.prototype.hasOwnProperty('getReceiver')}\n`);
            break;
        
        case 'Refund':
            const refundObj = new Refund(parseInt(inputsForObjectCreation[0]), inputsForObjectCreation[1]);
            ws.write(`Refund object created with amount ${refundObj.getAmount()} and sender ${refundObj.getSender()}\n`);
            if(refundObj.setAmount(updatedAmount)) {
                ws.write(`Amount updated to ${updatedAmount}\n`);
            } else {
                ws.write(`Amount not updated\n`);
            }
            refundObj.setSender(updatedSenderReceiver);
            ws.write(`Sender updated to ${updatedSenderReceiver}\n`);
            ws.write(`Refund object details - amount is ${refundObj.getAmount()} and sender is ${refundObj.getSender()}\n`);
            ws.write(`Refund.prototype has property setAmount: ${Refund.prototype.hasOwnProperty('setAmount')}\n`);
            ws.write(`Refund.prototype has property getAmount: ${Refund.prototype.hasOwnProperty('getAmount')}\n`);
            ws.write(`Refund.prototype has property setSender: ${Refund.prototype.hasOwnProperty('setSender')}\n`);
            ws.write(`Refund.prototype has property getSender: ${Refund.prototype.hasOwnProperty('getSender')}\n`);
            break;
        
        default:
            break;
    }
}

```
