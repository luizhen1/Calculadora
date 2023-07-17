<template>
   <div class="calculator">
        <ComponentsDisplay :value="displayValue"  />
        <ComponentsButton label="AC" triple @onClick="clearMemory" />
        <ComponentsButton label="/" operation @onClick="setOperation" />
        <ComponentsButton label="7" @onClick="addDigit" />
        <ComponentsButton label="8" @onClick="addDigit"/>
        <ComponentsButton label="9" @onClick="addDigit" />
        <ComponentsButton label="*" operation @onClick="setOperation"/>
        <ComponentsButton label="4" @onClick="addDigit" />
        <ComponentsButton label="5" @onClick="addDigit" />
        <ComponentsButton label="6" @onClick="addDigit"/>
        <ComponentsButton label="-" operation @onClick="setOperation"/>
        <ComponentsButton label="1" @onClick="addDigit" />
        <ComponentsButton label="2" @onClick="addDigit"/>
        <ComponentsButton label="3" @onClick="addDigit" />
        <ComponentsButton label="+" operation @onClick="setOperation" />
        <ComponentsButton label="0" double @onClick="addDigit" />
        <ComponentsButton label="." @onClick="addDigit" />
        <ComponentsButton label="=" operation @onClick="setOperation"/>
        
   </div>
</template>

<script>
import ComponentsButton from "../components/ComponentsButton"
import ComponentsDisplay from "../components/ComponentsDisplay"


export default {
    data: function(){
        return {
            displayValue: "0",
            clearDisplay: false,
            operation: null,
            values: [0, 0],
            current: 0
        }
    },
    components: { ComponentsButton, ComponentsDisplay },
    methods: {
        clearMemory(){
            Object.assign(this.$data, this.$options.data())
        },
       setOperation(operation) {
           if (this.current == 0) {
                this.operation = operation
                this.current = 1
                this.clearDisplay = true
           } else {
            const equals = operation == "="
            const currentOperation = this.operation

            try {
                this.values[0] = eval(
                    `${this.values[0]} ${currentOperation} ${this.values[1]}` 
                )
             }catch (e) {
                this.$emit('onError', e)
             }

             this.values[1] = 0

             this.displayValue = this.values[0]
             this.operation = equals ? null : operation
             this.current = equals ? 0 : 1
             this.clearDisplay = !equals

           }
        },
        addDigit(n) {
            if (n === "." && this.displayValue.includes(".")) {
                return
            }
            const clearDisplay = this.displayValue === "0"
            || this.clearDisplay
            const currentValue = clearDisplay ? "" : this.displayValue
            const displayValue = currentValue + n

            this.displayValue = displayValue
            this.clearDisplay = false
            this.values[this.current] = displayValue

            

        }
    }
}
</script>

<style>
.calculator {
    height: 320px;
    width: 235px;
    border-radius: 5px;
    overflow: hidden;
    
    display: grid;
    grid-template-columns: repeat(4,25%);
    grid-template-rows: 1fr 48px 48px 48px 48px 48px;


}


</style>