<template>
    <!-- Sample text -->
    <div class="w-100 mt-8">
        <!-- Language selection -->
        <div class="d-flex flex-wrap justify-space-between mb-1">
            <label class="mb-2">
                Sample text
                
                <v-menu offset-y nudge-top="-12px">
                    <template v-slot:activator="{ on, attrs }">
                        <v-icon class="ml-1" v-bind="attrs" v-on="on">mdi-information</v-icon>
                    </template>
                    <v-card outlined class="rounded-lg pa-4" width="320px">
                        Font size and space between lines can be set in the text reader.
                    </v-card>
                </v-menu>
            </label>

            <v-btn-toggle
                class="mb-1"
                v-model="selectedLanguage"
                mandatory
                rounded
                dense
                @change="updateSampleTextLanguage"
            >
                <v-btn 
                    v-for="(language, languageIndex) in languages" 
                    :key="`theme-${languageIndex}`"
                    small 
                    class="px-2" 
                >
                    {{ language }}
                </v-btn>
            </v-btn-toggle>
        </div>
        
        <!-- Text -->
        <div 
            :class="[
                'd-flex',
                'flex-wrap',
                'sample-text',
                'rounded-xl',
                'pa-4',
                selectedLanguage > 0 ? 'spaceless-language' : ''
            ] ">
            <div 
                v-for="(word, wordIndex) in sampleText"
                :key="'sample-text-word-' + wordIndex"
                :class="[
                    'word',
                    word.spaceAfter ? 'space-after' : '',
                    word.phraseStart ? 'phrase-start' : '',
                    word.phraseEnd ? 'phrase-end' : '',
                ]"
                :stage="word.stage"
                :phrasestage="word.phrase ? word.phrase : ''"
            >{{ word.word }}</div>

            <span class="d-block w-100 mt-4">Generated by ChatGPT.</span>
        </div>
    </div>
</template>


<script>
    export default {
        data: function() {
            return {
                sampleText: [],

                selectedLanguage: 0,
                languages: ['English', 'Japanese', 'Chinese', 'Thai'],
                multiLingualSampleTexts: {
                    english: "LinguaCafe is a platform designed to help you practice and improve your language skills through reading. Whether you're just starting to learn or looking to read more advanced material, there's something for everyone. You can explore articles, stories, and other reading materials that fit your level and interests. The platform makes learning feel more natural by exposing you to real language use in everyday contexts. You’ll also find helpful tools, like vocabulary lists and translation aids, that support your learning without interrupting the flow of your reading. Whether you're learning for fun or for more serious study, LinguaCafe is a simple way to stay connected with the language.",
                    japanese: "LinguaCafe は 、 読む ことで 言語 スキル を 練習 し 、 向上 させる ため の プラットフォーム です 。 初心者 から 上級者 まで 、 自分 の レベル に 合った 内容 を 見つける こと が できます 。 記事 や 物語 など 、 興味 や レベル に 合わせた 読み物 を 楽しむ こと が でき 、 日常的 な 文脈 で 使われる 言語 に 触れる こと が できます 。 語彙 リスト や 翻訳 ツール など 、 学習 を サポート する 便利 な ツール も あり 、 読む 楽しさ を 損なう こと なく 進められます 。 楽しく 学ぶ こと も 、 真剣 に 学びたい こと も できる LinguaCafe は 、 言語 と の つながり を 保つ シンプル な 方法 です 。",
                    chinese: "LinguaCafe 是 一 个 平台 ， 旨在 通过 阅读 帮助 你 练习 和 提高 语言 技能 。 无论 你 是 刚 开始 学习 ， 还是 希望 阅读 更 高级 的 材料 ， 都 能 找到 适合 自己 的 内容 。 你 可以 阅读 文章 、 故事 和 其他 符合 自己 水平 和 兴趣 的 材料 ， 接触 到 日常 生活 中 使用 的 语言 。 平台 还 提供 了 有用 的 工具 ， 比如 词汇表 和 翻译 工具 ， 帮助 你 在 阅读 的 同时 继续 学习 ， 而 不会 打断 阅读 的 流畅性 。 不论 是 为了 娱乐 还是 为了 更 严肃 的 学习 ， LinguaCafe 都 是 一 个 保持 与 语言 联系 的 简单 方法 。",
                    thai: "LinguaCafe คือ แพลตฟอร์ม ที่ ออกแบบ มา เพื่อ ช่วย ให้ คุณ ฝึกฝน และ พัฒนา ทักษะ ภาษา โดย การ อ่าน เนื้อหา ต่าง ๆ ไม่ว่า คุณ จะ เริ่ม เรียน ภาษา ใหม่ หรือ อยาก อ่าน เนื้อหา ขั้นสูง มากขึ้น ก็ สามารถ หา สิ่ง ที่ เหมาะสม ได้ ที่นี่ คุณ สามารถ อ่าน บทความ เรื่องราว และ เนื้อหา ต่าง ๆ ที่ ตรง กับ ระดับ และ ความสนใจ ของ คุณ โดย ได้ สัมผัส กับ การ ใช้ ภาษา ที่ เป็น ธรรมชาติ ใน ชีวิต ประจำวัน แพลตฟอร์ม ยัง มี เครื่องมือ ช่วยเหลือ เช่น รายการ คำศัพท์ และ เครื่องมือ แปล ที่ ช่วย สนับสนุน การ เรียนรู้ โดย ไม่ ขัดจังหวะ การ อ่าน ของ คุณ ไม่ว่า คุณ จะ เรียน เพื่อ ความ สนุก หรือ เพื่อ การ ศึกษา ที่ จริงจัง LinguaCafe เป็น วิธี ง่าย ๆ ที่ จะ เชื่อมต่อ กับ ภาษา ที่ คุณ เรียน อยู่",
                }

            }
        },
        mounted() {
            this.buildSampleText('english')
        },
        methods: {
            getStageDisplayName(stage) {
                stage = String(stage)
                let stageMapping = {
                    '2': 'new',
                    '1': 'ignored',
                    '0': 'known',
                    '-1': '1',
                    '-2': '2',
                    '-3': '3',
                    '-4': '4',
                    '-5': '5',
                    '-6': '6',
                    '-7': '7',
                }

                return stageMapping[stage];
            },
            updateSampleTextLanguage() {
                let selectedLanguage = this.languages[this.selectedLanguage].toLowerCase();
                this.buildSampleText(selectedLanguage)

            },
            buildSampleText(language) {
                this.sampleText = []
                let plainText = this.multiLingualSampleTexts[language]

                // generate object based sample text
                let textArray = plainText.split(' ')
                textArray.forEach((word, wordIndex) => {
                    let tempWord = {
                        word: word,
                        spaceAfter: this.selectedLanguage > 0 ? false : true,
                        stage: 0,
                    }

                    // remove space from previous word if current word is a point or a comma
                    if (wordIndex && [',', '.', '。', '，', '、'].includes(tempWord.word)) {
                        this.sampleText[wordIndex - 1].spaceAfter = false
                    }

                    // highlight random words
                    if (Math.random() * 100 < 40) {
                        tempWord.stage = Math.floor(Math.random() * 7 + 1) * -1
                    }

                    // set random words to new
                    if (Math.random() * 100 < 16) {
                        tempWord.stage = 2
                    }

                    // set random words to ignored
                    if (Math.random() * 100 < 16) {
                        tempWord.stage = 1
                    }

                    // create a phrase
                    if (wordIndex >= 2 && wordIndex <= 7) {
                        tempWord.stage = 0
                        tempWord.phrase = -7
                    }

                    tempWord.phraseStart = wordIndex === 2
                    tempWord.phraseEnd = wordIndex === 7


                    this.sampleText.push(tempWord)
                })
            },
        }
    }
</script>
