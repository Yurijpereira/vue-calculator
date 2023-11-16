<template>
    <div class="calculator">
        <div id="container-display">
            <input id="display" :value="displayValue" placeholder="0" type="text" disabled>
        </div>
        <div class="btns">
            <div class="container-btns">
                <Buttons @btn-add-value="changeDisplay" id="del-btn" btnValue="Del" />
                <Buttons @btn-add-value="compute" id="equals-btn" btnValue="=" />
            </div>
            <div class="container-btns">
                <Buttons @btn-add-value="changeDisplay" btnValue="7" />
                <Buttons @btn-add-value="changeDisplay" btnValue="8" />
                <Buttons @btn-add-value="changeDisplay" btnValue="9" />
                <Buttons @btn-add-value="changeDisplay" btnValue="+" />
            </div>
            <div class="container-btns">
                <Buttons @btn-add-value="changeDisplay" btnValue="4" />
                <Buttons @btn-add-value="changeDisplay" btnValue="5" />
                <Buttons @btn-add-value="changeDisplay" btnValue="6" />
                <Buttons @btn-add-value="changeDisplay" btnValue="-" />
            </div>
            <div class="container-btns">
                <Buttons @btn-add-value="changeDisplay" btnValue="1" />
                <Buttons @btn-add-value="changeDisplay" btnValue="2" />
                <Buttons @btn-add-value="changeDisplay" btnValue="3" />
                <Buttons @btn-add-value="changeDisplay" btnValue="/" />
            </div>
            <div class="container-btns">
                <Buttons @btn-add-value="changeDisplay" btnValue="C" />
                <Buttons @btn-add-value="changeDisplay" btnValue="0" />
                <Buttons @btn-add-value="changeDisplay" btnValue="." />
                <Buttons @btn-add-value="changeDisplay" btnValue="*" />
            </div>
        </div>
    </div>
</template>

<script>
import Buttons from './Buttons.vue';

export default {
    name: 'calculator',
    data() {
        return {
            displayValue: ''
        }
    },
    methods: {
        changeDisplay(btnValue) {
            let lastValue = this.displayValue[this.displayValue.length - 1];

            if (this.checkDuplicateSignal(btnValue)) return;

            if (this.checkDuplicatePoint(btnValue)) return;

            if((btnValue === '-' || btnValue === '.' || btnValue === '*' || btnValue === '/' || btnValue === '+') && lastValue === '-') return;
            if(btnValue === '-' && lastValue === '+') return;

            if (btnValue === "C" || this.displayValue === '/' || this.displayValue === '*') {
                this.displayValue = '';
            } else if (btnValue === "Del") {
                this.displayValue = this.displayValue.slice(0, -1);
            } else if (this.displayValue === '.') {
                this.displayValue = '0.';
            } else {
                this.displayValue += btnValue;
            }
        },
        compute() {
            let lastValue = this.displayValue[this.displayValue.length - 1];
            if (lastValue === '+' || lastValue === '-' || lastValue === '*' || lastValue === '/') return;

            let equal = eval(this.displayValue);

            if (equal === undefined) {
                equal = '0';
            } else if (equal === Infinity || isNaN(equal) || equal === -Infinity) {
                alert("Invalid mathematical operation");
                this.displayValue = '';
            } else {
                this.displayValue = equal;
            }
        },
        checkDuplicatePoint(btnValue) {
            let separateDisplay = this.displayValue.toString().split(/[\+\-\*\/]/);
            let lastSeparateDisplay = separateDisplay[separateDisplay.length - 1]
            if (lastSeparateDisplay.includes('.') && btnValue === '.') {
                return true;
            }
        },
        checkDuplicateSignal(btnValue) {
            const duplicateSignals = new RegExp(/[\+\*\/]$/);
            const lastCharacterSign = duplicateSignals.test(this.displayValue);
            const signTypedValue = duplicateSignals.test(btnValue);

            if (lastCharacterSign && signTypedValue) {
                return true;
            }
        }
    },
    components: {
        Buttons
    }
}
</script>

<style>
.calculator {
    flex-direction: column;
    background-color: #092c32;
    width: 700px;
    padding: 20px;
}

.btns {
    width: 100%;
}

.container-btns {
    display: flex;
}

#container-display {
    margin-bottom: 20px;
    width: 100%;
}

#display {
    font-size: 65px;
    width: 100%;
    padding: 20px;
    border: 2px solid #e5e5b9;
    border-radius: 10px;
    background-color: #18597a;
    color: #e5e5b9;
    text-align: end;
}

#display::placeholder {
    color: #e5e5b9;
    transition: .2s;
}
</style>