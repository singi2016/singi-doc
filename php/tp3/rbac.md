# rbac

##数据库
```sql
/*
 Navicat Premium Data Transfer

 Source Server         : localhost
 Source Server Type    : MySQL
 Source Server Version : 50542
 Source Host           : localhost
 Source Database       : singi

 Target Server Type    : MySQL
 Target Server Version : 50542
 File Encoding         : utf-8

 Date: 06/28/2016 13:23:15 PM
*/

SET NAMES utf8;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
--  Table structure for `role`
-- ----------------------------
DROP TABLE IF EXISTS `role`;
CREATE TABLE `role` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT COMMENT 'id',
  `name` varchar(10) NOT NULL COMMENT '角色名',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8;

-- ----------------------------
--  Records of `role`
-- ----------------------------
BEGIN;
INSERT INTO `role` VALUES ('1', '超级管理员'), ('2', '店长'), ('3', '员工');
COMMIT;

-- ----------------------------
--  Table structure for `role_rule`
-- ----------------------------
DROP TABLE IF EXISTS `role_rule`;
CREATE TABLE `role_rule` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `role_id` int(10) unsigned NOT NULL COMMENT '角色id',
  `rule_id` int(10) unsigned NOT NULL COMMENT '权限id',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=14 DEFAULT CHARSET=utf8;

-- ----------------------------
--  Records of `role_rule`
-- ----------------------------
BEGIN;
INSERT INTO `role_rule` VALUES ('1', '1', '13'), ('2', '1', '3'), ('3', '1', '4'), ('4', '1', '5'), ('5', '1', '6'), ('6', '1', '8'), ('7', '1', '9'), ('8', '2', '13'), ('9', '2', '5'), ('10', '3', '13'), ('11', '3', '8'), ('12', '2', '11'), ('13', '1', '12');
COMMIT;

-- ----------------------------
--  Table structure for `rule`
-- ----------------------------
DROP TABLE IF EXISTS `rule`;
CREATE TABLE `rule` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `name` varchar(10) NOT NULL COMMENT '权限名',
  `url` varchar(100) NOT NULL COMMENT '路由',
  `pid` int(10) unsigned NOT NULL COMMENT '父级id',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=14 DEFAULT CHARSET=utf8;

-- ----------------------------
--  Records of `rule`
-- ----------------------------
BEGIN;
INSERT INTO `rule` VALUES ('1', '签到管理', '', '0'), ('2', '用户管理', '', '0'), ('3', '用户', 'Admin/Member/index', '2'), ('4', '添加会员', 'Admin/Member/add', '2'), ('5', '会员列表', 'Admin/Member/MemberList', '2'), ('6', '删除会员', 'Admin/Member/del', '2'), ('7', '场馆管理', '', '0'), ('8', '基本信息', 'Admin/Studio/studioIndex', '7'), ('9', '场馆公告', 'Admin/Studio/noticeIndex', '7'), ('10', '课程管理', '', '0'), ('11', '课程列表', 'Admin/course/get', '10'), ('12', '课程日历', 'Admin/course/calendar', '10'), ('13', '签到', 'Admin/SignIn/sign', '1');
COMMIT;

-- ----------------------------
--  Table structure for `user`
-- ----------------------------
DROP TABLE IF EXISTS `user`;
CREATE TABLE `user` (
  `id` int(4) unsigned NOT NULL AUTO_INCREMENT,
  `name` varchar(10) DEFAULT NULL COMMENT '用户名',
  `sex` tinyint(2) DEFAULT '0' COMMENT '用户性别,0女，1男',
  `mobile` char(11) DEFAULT NULL COMMENT '手机号码',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8 COMMENT='用户id,主键';

-- ----------------------------
--  Records of `user`
-- ----------------------------
BEGIN;
INSERT INTO `user` VALUES ('1', '老秦', '1', '18877326071'), ('2', '林哥', '1', '15869325869'), ('3', '飘哥', '1', '14758963256');
COMMIT;

-- ----------------------------
--  Table structure for `user_role`
-- ----------------------------
DROP TABLE IF EXISTS `user_role`;
CREATE TABLE `user_role` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `uid` int(10) unsigned NOT NULL COMMENT '用户id',
  `role_id` int(10) unsigned NOT NULL COMMENT '角色id',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8;

-- ----------------------------
--  Records of `user_role`
-- ----------------------------
BEGIN;
INSERT INTO `user_role` VALUES ('1', '2', '1'), ('2', '3', '2'), ('3', '1', '3');
COMMIT;

SET FOREIGN_KEY_CHECKS = 1;

```

##获取角色所有权限方法
```php
function superAdmin(){
        $where['role_id'] = 1; //超级管理员
        $rule_ids = M('role_rule')->field('rule_id')->where($where)->select();
        $rule_id_str = implode(',',array_column($rule_ids,'rule_id'));

        $rule_where['_string'] = "id in ($rule_id_str)";
        $rules = M('rule')->where($rule_where)->select();
        $rule_last = array();
        $rule_parent = '';
        $rule_children = array();
        $flag = 0;
        foreach($rules as $i=>$v){
            $rule = M('rule')->find($v['pid']);
            if($rule){
                if($rule_parent['id'] == $rule['id']){
                    array_push($rule_children,$v);
                    $rule_parent['children'] = $rule_children;
                    $flag = 1;
                }else{
                    if($flag == 1 ){
                        $len = count($rule_last);
                        array_splice($rule_last,$len-1,1);
                        array_push($rule_last,$rule_parent);
                        $rule_parent = '';
                        $rule_children = array();
                    }
                    $rule_parent = $rule;
                    array_push($rule_children,$v);
                    $rule_parent['children'] = $rule_children;
                    array_push($rule_last,$rule_parent);

                }
            }
        }
        $this->assign('data',$rule_last);
        $this->display();
    }
```


