# Difference between toDateString and toDateTimeString

These methods is found in CarbonInterface that is `implemented` in Carbon class.
The methods are converted to string in Converter `trait` by using the format method in DateTime object.

## Difference

| Methods          |      Parameters               | Return String |
|----------        |:-------------:                |------:                 |
| toDateString     |  none                         |   '2022-07-26'         |
| toDateTimeString |  $unitPrecision = 'second'    |   '2012-07-27 12:49:06 |


```php
    public function toDateString()
    {
        return $this->rawFormat('Y-m-d');
    }

    public function toDateTimeString($unitPrecision = 'second')
    {
        return $this->rawFormat('Y-m-d '.static::getTimeFormatByPrecision($unitPrecision));
    }

    /**
     * @see https://php.net/manual/en/datetime.format.php
     *
     * @param string $format
     *
     * @return string
     */
    public function rawFormat($format)
    {
        return parent::format($format);
    }

    public static function getTimeFormatByPrecision($unitPrecision)
    {
        switch (static::singularUnit($unitPrecision)) {
            case 'minute':
                return 'H:i';
            case 'second':
                return 'H:i:s';
            case 'm':
            case 'millisecond':
                return 'H:i:s.v';
            case 'µ':
            case 'microsecond':
                return 'H:i:s.u';
        }

        throw new UnitException('Precision unit expected among: minute, second, millisecond and microsecond.');
    }

    public static function singularUnit(string $unit): string
    {
        $unit = rtrim(mb_strtolower($unit), 's');

        if ($unit === 'centurie') {
            return 'century';
        }

        if ($unit === 'millennia') {
            return 'millennium';
        }

        return $unit;
    }
```
