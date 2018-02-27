# phpAverageDistribution
对于给定总数，返回平均分配的最佳分配方案

/**
 * 根据给定的总数值返回每个单元的最值平均数
 *
 * @param integer $num 总共需要被平均的值
 * @param array   $data 提供的数据
 *
 * @example $num  = 12
 *           $data = [
 *                  "a" => 5,
 *                  "b" => 6,
 *                  "c" => 2,
 *                 ]
 *
 * @return [
 *          "a" => 5,
 *          "b" => 5,
 *          "c" => 2,
 *          ]
 */
```php
if (! function_exists('get_avg_data')) {
    function get_avg_data($num, array $data)
    {
        $sum = array_sum($data);
        // 如果数组内小于需要数值
        if ($num >= $sum){
            $reData = $data;
        } else {
            asort($data);
            $reData = handle_avg_data($num, $data);
        }

        return $reData;
    }
}
```

// 处理数据
```php
if (!function_exists('handle_avg_data')){
    function handle_avg_data(&$num, array &$data)
    {
        $n = count($data);
        $avg = (int)($num / $n);
        $y = $num % $n;
        $reData = [];
        $preData = $data;
        foreach ($data as $key => $value) {
            if ($value <= $avg){
                $reData[$key] = $value;
                unset($data[$key]);
                $num = $num - $value;
            }
        }
        if (count($preData) == count($data)){
            if ($y == 0){
                foreach ($data as $k => $v){
                    $reData[$k] = $avg;
                    unset($data[$k]);
                }
            } else {
                foreach ($data as $k => $v){
                    $reData[$k] = $avg + 1;
                    $num = $num -  $avg - 1;
                    unset($data[$k]);
                    break;
                }
            }
        }
        $reD = [];
        if (count($data) > 0){
            $reD = handle_avg_data($num, $data);
        }

        return array_merge($reData, $reD);
    }
}
```
