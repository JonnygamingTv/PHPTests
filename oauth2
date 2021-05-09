<?php
header('Location: https://discord.gg/');http_response_code(302);
if(isset($_GET["code"])){$cid = "client_id";$secret = "client_secret";$redirect_url = "https://JonHosting.com";
function do_post(string $url,string $params):string {
    $options = array(
        'http' => array(
            'header'  => "Content-type: application/x-www-form-urlencoded\r\n",
            'method'  => 'POST',
            'content' => $params
        )
    );
    $result = file_get_contents($url, false, stream_context_create($options));
    return $result;
}
function do_get(string $url,string $params):string {
    $options = array(
        'http' => array(
            'header'  => "Content-type: application/x-www-form-urlencoded\r\n$params\r\n",
            'method'  => 'GET'
        )
    );
    $result = file_get_contents($url, false, stream_context_create($options));
    return $result;
}
$ID = $_GET["code"];
$resultat = "";
$resultat = do_post('https://discord.com/api/v8/oauth2/token', "client_id=$cid&client_secret=$secret&grant_type=authorization_code&code=$ID&redirect_uri=$redirect_url");
if($resultat){$jres=false;
try{
    $jres = JSON_decode($resultat);
}catch(Exception $e){
    if($e){echo 'Caught exception: ',  $e->getMessage(), "\n";$jres=false;}
};
if($jres){
    $refresh=$jres->refresh_token;
    $access=$jres->access_token;
    $resultat2 = do_get('https://discord.com/api/v8/oauth2/@me', "authorization: Bearer $access");
    $jsobj=false;
    if($resultat2){
    try{$jsobj=JSON_decode($resultat2); $username=str_replace("<","&lt;",$jsobj->user->username); echo "<center><h1>Welcome to Discord sync, ". $username ."!</h1></center>";$id=str_replace(".","",str_replace("<","&lt;",$jsobj->user->id));file_put_contents("./discord/$id","1");http_response_code(301);}catch(Exception $e){}
    }else{echo "Failed.";}
}
}else{echo "Failed.";}
}
?>
