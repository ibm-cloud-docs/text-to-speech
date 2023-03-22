---

copyright:
  years: 2023
lastupdated: "2023-03-22"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Korean symbols
{: #koSymbols-new}

[IBM Cloud]{: tag-ibm-cloud}

The service supports the following symbols for Korean.

## Monophthongs
{: #koMonophthongs-new}

| SPR symbol | IPA symbol | IPA Unicode | Example words |
|:----------:|:----------:|:-----------:|---------------|
| a | a  \n ɐ  \n ɑ  \n ɞ  \n ʚ | 0061  \n 0250  \n 0251  \n 025E  \n 029A | 한 /h**a**n/ |
| A | ɛ  \n æ  \n ɜ | 025B  \n 00E6  \n 025C | 새로 /s**ɛ**ɾo/ |
| E | ʌ  \n ə  \n ɘ  \n ɵ | 028C  \n 0259  \n 0258  \n 0275 | 것 /k**ʌ**t/ |
| e | e | 0065 | 세 /s**e**/ |
| i | i  \n ı  \n ɨ  \n ɩ  \n ɪ | 0069  \n 0131  \n 0268  \n 0269  \n 026A | 시 /s**i**/ |
| o | o  \n ɒ  \n ɔ  \n ɤ | 006F  \n 0252  \n 0254  \n 0264 | 사고 /saɡ**o**/ |
| u | u  \n ɷ  \n ʉ  \n ʊ | 0075  \n 0277  \n 0289  \n 028A | 수 /s**u**/ |
| U | ɯ | 026F | 그 /k**ɯ**/ |
{: caption="Table 1. Monophthongs (Korean)"}

## Diphthongs
{: #koDiphthongs-new}

| SPR symbol | IPA symbol | IPA Unicode | Example words |
|:----------:|:----------:|:-----------:|---------------|
| ya | ja | U+006A + U+0061 | 약 /**ja**k/ |
| yA | jɛ | U+006A + U+025B | 얘기 /**jɛ**ɡi/ |
| yE | jʌ | U+006A + U+028C | 여섯 /**jʌ**sʌt/ |
| ye | je | U+006A + U+0065 | 예금 /**je**ɡɯm/ |
| yo | jo | U+006A + U+006F | 요즘 /**jo**dʑɯm/ |
| yu | ju | U+006A + U+0075 | 유독 /**ju**dok/ |
| wa | wa | 0077+0061| 봐  /p**wa**/ |
| wA | wɛ | 0077+025B | 왜 /**wɛ**/ |
| wE | wʌ | 0077+028C | 원인 /**wʌ**nin/ |
| we | we | 0077+0065 | 외부 /**we**bu/ |
| wi | wi  \n ɥi  \n y | 0077+0069  \n 0265+0069  \n 0079 | 행위 /hɛŋ**wi**/ |
| I | ɰi  \n ɯi | 0270+0069  \n 026F+0069 | 의사 /**ɰi**sa/ |
{: caption="Table 2. Diphthongs (Korean)"}

## Consonants
{: #koConsonants-new}

| SPR symbol | IPA symbol | IPA Unicode | Example words |
|:----------:|:----------:|:-----------:|---------------|
| c | dʑ  \n ʥ  \n tɕ  \n ʨ | 0064+0291  \n 02A5  \n 0074+0255  \n 02A8 | 여자 /jʌ**dʑ**a/ |
| 'cc' | t͈ɕ  \n tɕ͈  \n ʨ˭  \n ʨ͈ | 0074+0348+0255  \n 0074+0255+0348  \n 02A8+02ED  \n 02A8+0348 | 약점 /jak**t͈ɕ**ʌm/ |
| 'ch' | tɕʰ  \n ʨʰ | 0074+0255+02B0  \n 02A8+02B0 | 부착 /pu**tɕʰ**ak/ |
| h | h  \n ɦ | 0068  \n 0266 | 한 /**h**an/ |
| k | g  \n g̥  \n ɡ̥ | 006B  \n 0067+0325  \n 0261+0325 | 육 /ju**k**/ |
| 'kh' | kʰ | 006B+02B0 | 약한 /ja**kʰ**an/ |
| 'kk' | k˭  \n k͈ | 006B+02ED  \n 006B+0348 | 꼭 /**k͈**ok/ |
| l | l  \n ɭ | 006C  \n 026D | 오늘 /onɯ**l**/ |
| m | m | 006D | 마치 /**m**atɕʰi/ |
| n | n | 006E | 안 /a**n**/ |
| 'ng' | ŋ | 014B | 사상 /sasa**ŋ**/ |
| p | b  \n b̥  \n p  \n v | 0062  \n 0062+0325  \n 0070  \n 0076 | 보고 /**p**oɡo/ |
| 'ph' | f  \n pʰ | 0066  \n 0070+02B0 | 판매 /**pʰ**anmɛ/ |
| 'pp' | p˭  \n p͈ | 0070+02ED  \n 0070+0348 | 뿐 /**p͈**un/ |
| r | r  \n ɹ  \n ɾ  \n ʀ  \n ʁ | 0072  \n0279  \n 027E  \n 0280  \n 0281 | 주로 /tɕu**ɾ**o/ |
| s | sʰ  \n s  \n z  \n ɕ  \n ɕʰ | 0073+02B0  \n 0073  \n 007A  \n 0255  \n 0255+02B0 | 삼 /**s**am/ |
| 'ss' | s˭  \n s͈  \n ɕ˭  \n ɕ͈ | 0073+02ED  \n 0073+0348  \n 0255+02ED  \n 0255+0348 | 쓰고 /**s͈**ɯgo/ |
| t | d̥  \n d  \n t | 0064+0325  \n 0064  \n 0074 | 도 /**t**o/ |
| 'th' | tʰ | 0074+02B0 | 같은 /ka**tʰ**ɯn/ |
| 'tt' | t˭  \n t͈ | 0074+02ED  \n 0074+0348 | 때 /**t͈**ɛ/ |
| w | w | 0077 | 왜 /**w**ɛ/ |
| y | j | 006A | 야 /**j**a/ |
{: caption="Table 3. Consonants (Korean)"}
