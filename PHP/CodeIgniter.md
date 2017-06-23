# CodeIgniter
  
    |-----system                框架程序目录  
        |-----core              框架的核心程序  
            |-----CodeIgniter.php   引导性文件  
            |-----Common.php    加载基类库的公共函数  
            |-----Controller.php    基控制器类文件：CI_Controller  
            |-----Model.php     基模型类文件：CI_Model  
            |-----Config.php    配置类文件：CI_Config  
            |-----Input.php     输入类文件：CI_Input  
            |-----Output.php    输出类文件：CI_Output  
            |-----URL.php       URL类文件：CI_URl  
            |-----Router.php    路由类文件：CI_Router  
            |-----Loader.php    加载类文件：CI_Loader  
        |-----helpers           辅助函数  
            |-----url_helper.php    url相关的辅助函数，如：创建url的辅助函数  
            |-----captcha_helper.php创建图形验证码的辅助函数  
        |-----libraries         通用类库  
            |-----Pagination.php    通用分页类库  
            |-----Upload.php    通用文件上传类库  
            |-----Image_lib.php 通用图像处理类库  
            |-----Session.php   通用session类库  
        |-----language          语言包  
        |-----database          数据库操作相关的程序  
            |-----DB_active_rec.php 快捷操作类文件(ActiveRecord)  
        |-----fonts             字库  
          
    |-----application           项目目录  
        |-----core              项目的核心程序  
        |-----helpers           项目的辅助函数  
        |-----libraries         通用类库  
        |-----language          语言包  
        |-----config            项目相关的配置  
            |-----config.php    项目相关的配置文件     
            |-----database.php  数据库相关的配置文件  
            |-----autoload.php  设置自动加载类库的配置文件  
            |-----constants.php 常量配置文件  
            |-----routes.php    路由配置文件  
        |-----controllers       控制器目录  
            |-----welcome.php   控制器文件，继承CI_Controller  
        |-----models            模型目录  
            |-----welcome_model.php 模型文件，继承CI_Model  
        |-----views             视图目录  
            |-----welcome.php   视图模板文件，默认后缀名为.php  
        |-----cache             存放数据或模板的缓存文件  
        |-----errors            错误提示模板  
        |-----hooks             钩子，在不修改系统核心文件的基础上扩展系统功能  
        |-----third_party       第三方库  
        |-----logs              日志  
      
    |-----index.php             入口文件
  
#  MVC的理解
    M--模型，模型就是一个数据库类，一个模型对应一张表。
    V--视图，视图就是呈现出来的页面。
    C--控制器，用来操作视图的，相当于中介者，控制器把从M(模型)数据库中取出数据，再交给V(视图)呈现出来。

## C  
  控制器的创建位置：appcation/controllers/ 目录下
  控制器的命名规范： [详见PHP的命名规范](http://www.junhey.com/archives/135/)
  控制器文件的分目录管理  
  方法的命名规范：1、不能以list命名 2、方法名与类名不同名
  方法中如何获取GET方式提交过来的数据
  如:$username = $this->input->get_post('username', true);//获取post或get方式提交过来的数据  
  方法中如何获取POST方式提交过来的数据
  如:$username = $this->input->post('username', true);$username = $this->input-get_post('username', true);  
      
## V  
  视图的创建位置：appcation/views/ 目录下  
  视图的命名规范：login_view.php   login.html  
  如何在控制器中载入视图模板文件:$this->load->view("login"); $this->load->view("login.html");  
  如何在控制器中给视图模板文件传递数据:$this->load->view("login.html",$data);//extract函数  
  视图模板文件的分目录管理：$this->load->view("admin/category/addcategory.html");  
  
## M  
  模型的创建位置：application/models 目录下  
  模型的命名规范：不区分大小写，建议表名和功能类似  
  如何在控制器中载入模型（自动加载和手动加载）：$this->load->model("user_model");  
  模型文件的分目录管理:$this->load->model("admin/user_model");  
  
## codeigniter框架中如何扩展控制器、模型  
  基控制器的扩展:class Common extends CI_Controller{}  
  基模型的扩展:class Model extends CI_Model{}   
  
## codeigniter框架中辅助函数  
  辅助函数的位置：application/helpers 目录 或 system/helpers 目录  
  如何在控制器中载入辅助函数：$this->load->helper("url");//载入url_helper.php文件  
  自定义辅助函数  
  辅助函数的扩展  
  辅助函数的载入机制：首先考虑载入application/helpers 目录下的文件，再考虑载入system/helpers 目录下的文件  
  页面的跳转：header("location:".site_url("admin/login/"));//创建一个url，并跳转
  
## codeigniter框架中的配置文件  
  配置文件的位置：application/config/ 目录下  
  如何在CI项目的控制器中载入配置文件（手动载入和自动载入）：$this->config->load("pagination");  
  如何自定义配置文件：application/config/pagination.php    配置项变量名必须是 $config['配置项']  
  配置文件中配置项的命名规范：$config['配置项']  
  如何动态给配置项设置值：$this->config->set_item("配置项","配置项值");  
  如何将分页配置写到配置文件中  
  如何将配置文件合并：$this->config->load("pagination",true);//参数2：true
  
## codeigniter框架中的通用类库  
  通用类库的位置：application/libraries/ 目录 system/libraries/ 目录  
  如何在ci项目的控制器中载入通用类库：$this->load->library("upload");//文件上传类库的载入  
  通用类库的载入机制：优先考虑载入application/libraries/ 目录下类库，其次考虑载入 system/libraries 目录下类库  
  分页类库的载入（定制分页风格）:$this->load->library("pagination");  
  列表页分页功能的完成
  
### 显示最后一条查询的sql语句：主要用于在连贯操作时，检测拼接的sql语句是否正确
``` php 
 echo $this->db->last_query();//如:select * from pt_users where uid>10 order by datetime desc limit 0,10
```
### 缓存驱动的加载方式  
``` php
    $this->load->driver('cache', array('adapter' => 'memcached'));//加载缓存驱动或缓存适配器,当前为memcached缓存;注意:CI框架只支持memcached,不支持memcache,windows操作系统下只有memcache扩展 
    $this->load->driver('cache', array('adapter' => 'file'));//加载缓存驱动或缓存适配器,当前为file缓存 
    $this->load->driver('cache', array('adapter' => 'redis'));//加载缓存驱动或缓存适配器,当前为redis缓存  
    $this->load->driver('cache', array('adapter' => 'apc', 'backup' =>'file'));//优先选择apc缓存,file文件缓存作为替代方案;如果服务器不支持apc缓存时,选择file文件缓存
```




> 访问：localhost/项目文件名/入口文件(index.php)/控制器名/控制器中的方法名

#### 调试开启：$this->output->enable_profiler(TRUE);

#### base_url() 用来创建静态资源的地址，如JS、CSS等地址需要用该函数来生成。site_url() 用来创建跟控制器地址相关的URL

# CI框架通用Model类封装

``` php
<?php defined('BASEPATH') or exit('No direct script access allowed');
/**
 * 数据库CRUD操作扩展(models)
 * Model.php
 * ============================================================
 * 简化数据库CRUD基本功能操作
 * ============================================================
 * @author hejun(2511906352@qq.com)
 */
class MY_Model extends CI_Model
{
	protected $table;//当前操作的data table
	/**
	 *	构造函数
	 *  $table:数据表
	 */
	function __construct($table = '',$database = 'default')
	{
		parent::__construct();
		date_default_timezone_set('Asia/Shanghai');
		$this->table = $table;
	}
	/**
	 *	添加数据
	 *  $dataArr:(array)插入的数据
	 *  return:当前插入的数据id
	 */
	function insert($dataArr)
	{
		$this->db->insert($this->table, $dataArr);
		return $this->db->insert_id();
	}
	/**
	 *	修改数据
	 *  $dataArr:(array)更新的数据
	 *  $whereArr:(array)更新的条件
	 *  return:更新的数据条数
	 */
	function update($dataArr, $whereArr)
	{
		$this->db->where($whereArr);
		$this->db->update($this->table, $dataArr);
		return $this->db->affected_rows();
	}
	/**
	 *	删除数据
	 *  $whereArr:(array)删除的条件
	 *  return:删除的数据条数
	 */
	function delete($whereArr)
	{
		$this->db->where($whereArr);
		$this->db->delete($this->table); 
		return $this->db->affected_rows();
	}
	/**
	 *	查询并返回一条数据
	 *  $whereArr:(array)查询的条件
	 *  $type:返回结果类型，默认为obj格式，arr为数组格式
	 *  return:查询结果
	 */
	function row($whereArr, $type='arr', $orderby = "",$fieldsArr="")
	{
		if(!empty($fieldsArr)){
			if (is_array($fieldsArr))
			{
				foreach($fieldsArr as $key => $value)
				{
					$this->db->select($value, FALSE);
				}
			}else{				
				$this->db->select($fieldsArr);
			}
		}
		$this->db->where($whereArr);
		if(!empty($orderby)){
			$orderby = str_replace("@"," ",$orderby);
			$this->db->order_by($orderby);
		}
		$query = $this->db->get($this->table);
		if($type=='obj')return $query->row();
		elseif($type=='arr')return $query->row_array();
	}
	
	 /**
	 *	查询并返回多条数据
	 *  $whereArr:(array)查询的条件
	 *  $type:返回结果类型，默认为obj格式，arr为数组格式
	 *  $num:单页显示的条数
	 *  $page:当前页数
	 *  $orderby:排序条件
	 *  return:查询结果
	 */
	function result($whereArr, $page = 1, $num = 10, $orderby = "", $type='arr',$joinArr='',$fieldsArr="")
	{
		if(!empty($fieldsArr)){
			if (is_array($fieldsArr))
			{
				foreach($fieldsArr as $key => $value)
				{
					$this->db->select($value, FALSE);
				}
			}else{
				$this->db->select($fieldsArr);
			}
		}
		if($page==0) $page=1;
		$offset=($page-1)*$num;
		$this->db->where($whereArr);
		if(!empty($orderby)){
			$orderby = str_replace("@"," ",$orderby);
			$this->db->order_by($orderby);
		}
		if(!empty($joinArr)){
			$this->db->join($joinArr[0], $joinArr[1],$joinArr[2]);
		}
		$query = $this->db->get($this->table,$num,$offset);
		if($type=='obj')return $query->result();
		elseif($type=='arr')return $query->result_array();
	}
	
	/**
	 *	查询并返回所有数据
	 *  $whereArr:(array)查询的条件
	 *  $type:返回结果类型，默认为obj格式，arr为数组格式
	 *  $orderby:排序条件
	 *  return:查询结果
	 */
	function all($whereArr=array(), $orderby = "", $type='arr',$fieldsArr="")
	{
		if(!empty($fieldsArr)){
			if (is_array($fieldsArr))
			{
				foreach($fieldsArr as $key => $value)
				{
					$this->db->select($value, FALSE);
				}
			}else{
				$this->db->select($fieldsArr);
			}
		}
		$this->db->where($whereArr);
		if(!empty($orderby)){
			$orderby = str_replace("@"," ",$orderby);
			$this->db->order_by($orderby);
		}
		$query = $this->db->get($this->table);
		if($type=='obj')return $query->result();
		elseif($type=='arr')return $query->result_array();
	}
	
	/**
	 *	查询数据条数
	 *  $whereArr:(array)查询的条件
	 *  return:查询结果数据条数
	 */
	function num_rows($whereArr,$joinArr='')
	{		
		$this->db->where($whereArr);
		if(!empty($joinArr)){
			$this->db->join($joinArr[0], $joinArr[1],$joinArr[2]);
		}
		$query = $this->db->get($this->table);
		return $query->num_rows();
	}
}
```
