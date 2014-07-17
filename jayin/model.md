### model
主要是各种数据库的处理


### 如何写一个model
直接上例子
文件目录 model/account/api.php 
```php
    //注意类命名方式，跟文件目录相关，不然无法加载
    class ModelAccountApi extends Model {
	public function login($username, $password) {
		$query = $this->db->query("SELECT * FROM `" . DB_PREFIX . "api` WHERE username = '" . $this->db->escape($username) . "' AND password = '" . $this->db->escape($password) . "' AND status = '1'");

		return $query->row;
	}
}


```



