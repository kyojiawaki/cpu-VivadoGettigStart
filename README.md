# cpu.v
VivadoでCPUを作成

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
