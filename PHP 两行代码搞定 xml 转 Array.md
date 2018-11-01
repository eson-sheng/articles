```php
/**
* 将xml转为array
* @param string $xml
*/
public function xml_for_arr($xml)
{
    if(!$xml){
    return "xml数据异常！";
    // return FALSE;
}
//将XML转为array
//禁止引用外部xml实体
libxml_disable_entity_loader(TRUE);
return json_decode(json_encode(simplexml_load_string($xml, 'SimpleXMLElement', LIBXML_NOCDATA)), TRUE);
}
```