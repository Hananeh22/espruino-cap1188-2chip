// Registers
var REG = {
    CONTROL_MAIN          : 0x00,
    CONTROL_SENSITIVITY   : 0x1F,
    STATUS_GENERAL        : 0x02,
    STATUS_SENSOR         : 0x03,
    SENSOR_ENABLE         : 0x21,
    SENSOR_SAMPLING       : 0x24,
    SENSOR_CALIBRATE      : 0x26,
    SENSOR_BASE           : 0x50,
    SENSOR_DELTA          : 0x10,
};

function CAP1188(_i2c) {
    this.i2c = _i2c;
    this.addr = 0x29;
}

CAP1188.prototype.readBase = function(sensor) {
    this.i2c.writeTo(this.addr, (REG.SENSOR_BASE + sensor - 1));
    return this.i2c.readFrom(this.addr, 1)[0];
}

CAP1188.prototype.readDelta = function(sensor) {
    this.i2c.writeTo(this.addr, (REG.SENSOR_DELTA + sensor - 1));
    return this.i2c.readFrom(this.addr, 1)[0];
};

CAP1188.prototype.enable = function(sensor) {
    this.i2c.writeTo(this.addr, [REG.SENSOR_ENABLE, (sensor - 1) << 1]);
}

CAP1188.prototype.calibrate = function(sensor) {
    this.i2c.writeTo(this.addr, [REG.SENSOR_CALIBRATE, (sensor - 1) << 1]);
};

CAP1188.prototype.setSensitivity = function(mult) {
    var mult_byte;
    switch (mult) {
        case 128: mult_byte = 0x0F;
        case 64 : mult_byte = 0x1F;
        case 32 : mult_byte = 0x2F;
        case 16 : mult_byte = 0x3F;
        case 8  : mult_byte = 0x4F;
        case 4  : mult_byte = 0x5F;
        case 2  : mult_byte = 0x6F;
        case 1  : mult_byte = 0x7F;
        default : mult_byte = 0x2F;
    }
    this.i2c.writeTo(this.addr, [REG.CONTROL_SENSITIVITY, mult_byte]);
}

exports.connect = function (_i2c) {
    return new CAP1188(_i2c);
};
