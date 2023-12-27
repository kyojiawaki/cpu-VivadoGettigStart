# cpu.v
VivadoでCPUを作成

## 1. 組み合わせ回路のRTL部品
1. デコーダ(dec.v)
* 機能
  * 3入力、8出力のデコーダ
  * 3ビットの信号aを入力し、2進数として解釈し、出力信号xの対応するビットを1とする.
2. エンコーダ(enc.v)
* 機能
  * 8入力、4出力のプライオリティエンコーダ
  * 入力aが0でなければ(どれか一つが1であれば)、x[3]に1を出力する
  * 入力aの各ビットの中で、値が1であるビットに対応した2進数をx[2:0]に出力する
  * 同時に二つ以上のビットが1である場合、ビット0に近い方を優先する
 3. マルチプレクサ(mux.v)
 * 機能
   * 8ビットの入力a、bのどちらか一つがsによって選択され、xに出力されるマルチプレクサ
   * sが1であればaをxに、sが0であればbをxに出力する 
4. コンパレータ(cmp.v)
* 機能
  * 8ビットの入力a、bを比較し、結果をgt, lt, eqに出力するコンパレータである。
  * 入力aとbを比較し、同じであればeqに1を出力し、そうでなければ0を出力する。
  * 入力aとbを比較し、aがbより大きければgtに1を出力し、そうでなければ0を出力する。
  * 入力aとbを比較し、aがbより小さければltに1を出力し、そうでなければ0を出力する。
5. 加算器(add.v)
* 機能
  * キャリーイン、キャリーアウト付きの8ビット入力、8ビット出力の加算器
  * 入力a、bとキャリーインcinを加算し、結果をキャリーアウトcoとxに出力する
6.  シフタ(shift.v)
* 機能
  * 入力aをdで示された方向にnビットシフトしてxに出力するシフタである
  * dが0のとき右、dが1のとき左にシフトする
  * シフトした後のビットには0を入れる
7. 乗算器(mult.v)
* 機能
  * 8ビットの入力a、bを乗算し、結果を16ビットのxに出力する乗算器である
8. ALU(alu.v)
* 機能
  * 入力はopcodeに従ってaccumとdataを演算し、alu_outに出力するALUである
  * ALUは、Arithmetic Logic Unit(算術演算ユニット)のことである
9. パリティジェネレータ(parity.v)
* 機能
  * 入力aの奇数パリティをxに出力するパリティジェネレータである
  * 入力aの奇数パリティは、aの各ビットの中で1であるビットの数が奇数であれば1となり、偶数であれば0となる
  * 一般的に、データにパリティを付けておくことによりデータの1ビットの誤りを検出できる
## 2. 順序回路のRTL部品
1. 同期リセット付きレジスタ
* 機能
  * 8ビット、同期リセット付き、エッジトリガのレジスタ
  * クロックclkの立ち上がりエッジに同期して、リセットrstが0のときqを0とする(同期リセットする)
  * クロックclkの立ち上がりエッジに同期して、リセットrstが1のときdの値をqに出力する
  * 同期リセット付きレジスタのタイミング図を以下に示す
![スクリーンショット 2023-12-28 001808](https://github.com/kyojiawaki/cpu.v/assets/130772825/5bf94f9f-96f8-4b88-a079-328b1d2cc748)
