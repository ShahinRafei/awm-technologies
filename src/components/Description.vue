<script>
export default {
    // data
    data() {
        return {
            description: '',
        };
    },

    // methods
    methods: {
        isBalanced(text = this.description) {
            const stack = [];
            const openingBrackets = ['(', '[', '{'];
            const closingBrackets = [')', ']', '}'];
            const bracketMap = {
                ')': '(',
                ']': '[',
                '}': '{',
            };

            for (let i = 0; i < text.length; i++) {
                let char = text[i];
                if (openingBrackets.includes(char)) {
                    stack.push({ bracket: char, position: i });
                } else if (closingBrackets.includes(char)) {
                    const top = stack.pop();
                    if (!top || top.bracket !== bracketMap[char]) {
                        return false;
                    }
                }
            }

            return stack.length === 0;
        },

        checkForQuestionMark(event) {
            const newText = event.target.value;
            if (newText.includes('?')) {
                event.target.nextSibling.innerText = this.isBalanced(newText) ? 'The text is balanced.' : 'The text is not balanced.';
            }
        }
    },

};
</script>

<template>
    <input v-model="description" @input="checkForQuestionMark" type="text" id="description">
    <p></p>
</template>