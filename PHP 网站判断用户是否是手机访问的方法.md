# PHP网站判断用户是否是手机访问的方法
有些时候，我们需要判断用户是否用手机访问，如果是手机的话，就跳转到指定的手机友好页面。这里就介绍一下，如何判断用户是否用手机访问。

### 自定义的函数如下：
```php
$agent = check_wap();
if( $agent )
{
    header('Location: http://www.jb51.net');
    exit;
}
  
// check if wap
function check_wap()
{
    // 先检查是否为wap代理，准确度高
    if(stristr($_SERVER['HTTP_VIA'],"wap")){
        return true;
    }
    // 检查浏览器是否接受 WML.
    elseif(strpos(strtoupper($_SERVER['HTTP_ACCEPT']),"VND.WAP.WML") > 0){
        return true;
    }
    //检查USER_AGENT
    elseif(preg_match('/(blackberry|configuration\/cldc|hp |hp-|htc |htc_|htc-|iemobile|kindle|midp|mmp|motorola|mobile|nokia|opera mini|opera |Googlebot-Mobile|YahooSeeker\/M1A1-R2D2|android|iphone|ipod|mobi|palm|palmos|pocket|portalmmm|ppc;|smartphone|sonyericsson|sqh|spv|symbian|treo|up.browser|up.link|vodafone|windows ce|xda |xda_)/i', $_SERVER['HTTP_USER_AGENT'])){
        return true;
    }
    else{
        return false;
    }
}
```
再来一个从PHP框架剥离的判断是否为手机移动终端的函数：（经过测试，很全面，推荐使用）
```php
function is_mobile_request() 
{ 
 $_SERVER['ALL_HTTP'] = isset($_SERVER['ALL_HTTP']) ? $_SERVER['ALL_HTTP'] : ''; 
 $mobile_browser = '0'; 
 if(preg_match('/(up.browser|up.link|mmp|symbian|smartphone|midp|wap|phone|iphone|ipad|ipod|android|xoom)/i', strtolower($_SERVER['HTTP_USER_AGENT']))) 
  $mobile_browser++; 
 if((isset($_SERVER['HTTP_ACCEPT'])) and (strpos(strtolower($_SERVER['HTTP_ACCEPT']),'application/vnd.wap.xhtml+xml') !== false)) 
  $mobile_browser++; 
 if(isset($_SERVER['HTTP_X_WAP_PROFILE'])) 
  $mobile_browser++; 
 if(isset($_SERVER['HTTP_PROFILE'])) 
  $mobile_browser++; 
 $mobile_ua = strtolower(substr($_SERVER['HTTP_USER_AGENT'],0,4)); 
 $mobile_agents = array( 
    'w3c ','acs-','alav','alca','amoi','audi','avan','benq','bird','blac', 
    'blaz','brew','cell','cldc','cmd-','dang','doco','eric','hipt','inno', 
    'ipaq','java','jigs','kddi','keji','leno','lg-c','lg-d','lg-g','lge-', 
    'maui','maxo','midp','mits','mmef','mobi','mot-','moto','mwbp','nec-', 
    'newt','noki','oper','palm','pana','pant','phil','play','port','prox', 
    'qwap','sage','sams','sany','sch-','sec-','send','seri','sgh-','shar', 
    'sie-','siem','smal','smar','sony','sph-','symb','t-mo','teli','tim-', 
    'tosh','tsm-','upg1','upsi','vk-v','voda','wap-','wapa','wapi','wapp', 
    'wapr','webc','winw','winw','xda','xda-'
    ); 
 if(in_array($mobile_ua, $mobile_agents)) 
  $mobile_browser++; 
 if(strpos(strtolower($_SERVER['ALL_HTTP']), 'operamini') !== false) 
  $mobile_browser++; 
 // Pre-final check to reset everything if the user is on Windows 
 if(strpos(strtolower($_SERVER['HTTP_USER_AGENT']), 'windows') !== false) 
  $mobile_browser=0; 
 // But WP7 is also Windows, with a slightly different characteristic 
 if(strpos(strtolower($_SERVER['HTTP_USER_AGENT']), 'windows phone') !== false) 
  $mobile_browser++; 
 if($mobile_browser>0) 
  return true; 
 else
  return false;
```