# bit-register
an implementation of c/c++ bit fields in javascript.

Following @OneLoneCoders nes emulator on youtube I needed to create the registers used in various parts of my JavaScript version of the emulator.
So I came up with this the base class basically recreates a union of a struct with bit fields and an integer.

## Example Use
```JS
/**
 * Class represeting the status register
 * @extends Register
 */
class StatusReg extends Register {  
  /**
   * creates a Status Register
   */
  constructor() {
    super(8, {
      UNU: new MapItem('unused',          0x1F, 0, 0x1F),
      SOF: new MapItem('sprite_overflow', 0x20, 5, 0x1),
      SZH: new MapItem('sprite_zero_hit', 0x40, 6, 0x1),
      VBL: new MapItem('vertical_blank',  0x80, 7, 0x1)
    });
  }
}

let status = new StatusReg();
status.sprite_overflow = 1;
// the resulting value stored in the reg variable is 0x20;
status.reg = 0;
// clears the status setting all fields to 0;
status.reg = 82;
status.unused; // would be 12 
status.sprite_zero_hit; // would be 1
```
This would be similar to:
```c++
union {
  struct {
    unit8_t unused: 5; // 5 bits
    unit8_t sprite_overflow: 1; // 1 bit
    unit8_t sprite_zero_hit: 1; // 1 bit
    unit8_t vertical_blank: 1; // 1 bit
  };
  unit8_t reg; // 8 bits
} status;
```
