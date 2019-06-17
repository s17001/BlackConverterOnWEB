<template>
    <div>
        <div>ここは説明文です</div>
        <div><textarea v-model="inputs" v-on:keyup="ConvertingInput" name="" id="input" cols="30" rows="10"></textarea></div>
        <div><textarea v-model="output" id="output" cols="30" rows="10"></textarea></div>
        <p>{{inputs}}</p>
        <button @click="ConvertingInput"></button>
    </div>
</template>

<script>
    const blackConstructor = `__=-~-~[-~[]];_=[...{}+[]][__+__- -~[]]+[...{}+[]][-~[]]+([][""]+[])[-~[]]+(([]==[])+[])[__]+(-~[]/[]+[])[__+__]+(!![]+[])[-~[]]+([][""]+[])[+[]]+[...{}+[]][__+__- -~[]]+(!![]+[])[+[]]+[...{}+[]][-~[]]+(!![]+[])[-~[]];`;

    const charTable = {
        " ": "' '",
        "\n": "[]",
        t: "(!![]+[])[-[]]",
        r: "(!![]+[])[-~[]]",
        u: "([]['']+[])[-[]]",
        e: "(!![]+[])[-~-~[-~[]]]",
        f: "(![]+[])[-[]]",
        a: "(![]+[])[-~[]]",
        l: "(![]+[])[-~[-~[]]]",
        s: "(![]+[])[-~[-~[-~[]]]]",
        n: "([]['']+[])[-~[]]",
        d: "([]['']+[])[-~[-~[]]]",
        i: "([]['']+[])[(-~[]<<-~[-~[]])+-~[]]",
        I: "(~[]/-[]+[])[-[]]",
        y: "(- -~[]/-[]+[])[(-~[]+[]+-~[]>>-~[])+(-~[]<<-~[])]",
        o: "([...{}+{}])[-~[]]",
        b: "([...{}+{}])[-~[]<<-~[]]",
        j: "([...{}+{}])[-~-~[-~[]]]",
        c: "([...{}+{}])[(-~[]+[]+-~[]>>-~[])]",
        N: "(''/''+[])[-[]-[]]",
        "0": "([]-[]+[])",
        "1": "(-~[])",
        "2": "(-~[-~[]])",
        "3": "(__)",
        "4": "(-~[__])",
        "5": "(-~[]+[]+-~[]>>-~[])",
        "6": "(__+__)",
        "7": "((-~[]+[]+-~[]>>-~[])+(-~[]<<-~[]))",
        "8": "(-~[__]*-~-~[])",
        "9": "(__*__)",

    };

    const replaceBlackCode = string => {
        return string.replace(/./gsu, char => charTable[char] || char);
    };

    const createReturnUTF = string => {
        return `(!![]+[])[-~[]]+(!![]+[])[__]+(!![]+[])[+[]]+(!![]+[])[-~[-~[]]]+(!![]+[])[-~[]]+([]['']+[])[-~[]]+' \"'+'\\\\' +([]['']+[])[[]-[]] +'{' +${string}+ '}'+'\"'`;
    };

    const wrapper = string => {
        return `[][_][_](${string})()`;
    };

    export default {
        name: "Converter",
        data() {
            return {
                inputs:'',
                output:''
            }
        },
        methods:{
            ConvertingInput(){
                const processingData =[]

                for (const input of [...this.inputs+[]]) {

                    //使える文字なら => 置き換える
                    if (input in charTable) {
                        processingData.push(charTable[input]);
                        continue;
                    }

                    // charCode単位でイテレートする
                    for (let i = 0, l = input.length; i < l; ++i) {
                        //使えない文字なら => utf8に変換して、数字を記号化する
                        const parsedArr = [...(input.charCodeAt(i).toString(16) + [])];

                        //ここで形成した配列をさらにreplaceBlackCodeしてまとめる
                        const flamedArr = parsedArr.map(replaceBlackCode);

                        const utf8code = wrapper(createReturnUTF(flamedArr.join("+")));
                        processingData.push(utf8code);
                    }
                }
                this.output = blackConstructor
                this.output += processingData.join('+')
            }
        }
    }
</script>

<style scoped>

</style>