# fastwego/wxwork 

A fast [wxwork](https://work.weixin.qq.com/api/doc) development sdk written in Golang

[![GoDoc](https://pkg.go.dev/badge/github.com/fastwego/wxwork?status.svg)](https://pkg.go.dev/github.com/fastwego/wxwork?tab=doc)
[![Go Report Card](https://goreportcard.com/badge/github.com/fastwego/wxwork)](https://goreportcard.com/report/github.com/fastwego/wxwork)

## 快速开始 & demo

```shell script
go get github.com/fastwego/wxwork
```

```go

// 创建企业实例
Corp = corporation.New(corporation.Config{Corpid: "CROPID"})

//创建通讯录 App
ContactApp = Corp.NewApp(corporation.AppConfig{
    AgentId:        "AGENTID",
    Secret:         "SECRET",
    Token:          "TOKEN",
    EncodingAESKey: "EncodingAESKey",
})

// 通讯录管理 -> 获取部门成员详情
params := url.Values{}
params.Add("department_id", "10086")
resp, err := contact.UserList(ContactApp, params)
```

完整演示项目：

[https://github.com/fastwego/wxwork-demo](https://github.com/fastwego/wxwork-demo)

## 架构设计

![sdk](corporation/doc/img/sdk.jpg)

## 框架特点

### 快速

「快」作为框架设计的核心理念，体现在方方面面：

- 使用 Go 语言，开发快、编译快、部署快、运行快，轻松服务海量用户
- 丰富的[文档](https://pkg.go.dev/github.com/fastwego/wxwork) / [教程](corporation/doc/SUMMARY.md) 和 [演示代码](https://github.com/fastwego/wxwork-demo) ，快速上手，5 分钟即可搭建一套完整的微信服务
- 独立清晰的模块划分，快速熟悉整个框架，没有意外，一切都是你期望的样子
- 甚至连框架自身的大部分代码也是自动生成的，维护更新快到超乎想象

### 符合直觉

作为第三方开发框架，尽可能贴合官方文档和设计，不引入新的概念，不给开发者添加学习负担

### 简洁而不过度封装

作为具体业务和企业微信之间的中间层，专注于通道的角色：帮业务把配置/材料投递到企业微信，将企业微信响应/推送透传回业务

至于 [AccessToken 管理](corporation/doc/access_token.md) 和 [消息加解密处理](corporation/doc/message.md)，框架内部完成得干净利落，开发者甚至觉察不到存在

### 官方文档就是最好的文档

每个接口的注释都附带官方文档的链接，让你随时翻阅，省时省心

### 完备的单元测试

100% 覆盖每一个接口，让你每一次调用都信心满满

### 详细的日志

每个关键环节都为你完整记录，Debug 倍轻松，你可以自由定义日志输出，甚至可以关闭日志

### 多账号支持

一套服务支持多个企业微信账号，轻松成为第三方开发服务平台，业务节节高

### 支持服务集群

单台服务器支撑不住访问流量/想提高服务可用性？

只需 [设置 GetAccessTokenFunc 方法](https://pkg.go.dev/github.com/fastwego/wxwork/corporation?tab=doc#App.SetGetAccessTokenHandler) ，从中控服务获取 AccessToken，即可解决多实例刷新冲突/覆盖的问题

### 活跃的开发者社区

FastWeGo 是一套完整的微信开发框架，包括公众号、开放平台、微信支付、企业微信、小程序、小游戏等微信服务，拥有庞大的开发者用户群体

你遇到的所有问题几乎都可以在社区找到解决方案

## 参与贡献

欢迎提交 pull request / issue / 文档，一起让微信开发更快更好！

Faster we go together!

[加入开发者交流群](https://github.com/fastwego/fastwego.dev#%E5%BC%80%E5%8F%91%E8%80%85%E4%BA%A4%E6%B5%81%E7%BE%A4)

## 接口列表

- 开发辅助(util)
	- [获取企业微信API域名IP段](https://work.weixin.qq.com/api/doc/90000/90135/92520) 
		- [GetApiDomainIp (/cgi-bin/get_api_domain_ip)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/util?tab=doc#GetApiDomainIp)
	- [获取企业微信服务器的ip段](https://work.weixin.qq.com/api/doc/90000/90135/90238) 
		- [GetCallbackIp (/cgi-bin/getcallbackip)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/util?tab=doc#GetCallbackIp)
- 通讯录管理(contact)
	- [创建成员](https://work.weixin.qq.com/api/doc/90000/90135/90195) 
		- [UserCreate (/cgi-bin/user/create)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#UserCreate)
	- [读取成员](https://work.weixin.qq.com/api/doc/90000/90135/90196) 
		- [UserGet (/cgi-bin/user/get)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#UserGet)
	- [更新成员](https://work.weixin.qq.com/api/doc/90000/90135/90197) 
		- [UserUpdate (/cgi-bin/user/update)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#UserUpdate)
	- [删除成员](https://work.weixin.qq.com/api/doc/90000/90135/90198) 
		- [UserDelete (/cgi-bin/user/delete)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#UserDelete)
	- [批量删除成员](https://work.weixin.qq.com/api/doc/90000/90135/90199) 
		- [UserBatchDelete (/cgi-bin/user/batchdelete)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#UserBatchDelete)
	- [获取部门成员](https://work.weixin.qq.com/api/doc/90000/90135/90200) 
		- [UserSimpleList (/cgi-bin/user/simplelist)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#UserSimpleList)
	- [获取部门成员详情](https://work.weixin.qq.com/api/doc/90000/90135/90201) 
		- [UserList (/cgi-bin/user/list)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#UserList)
	- [userid与openid互换](https://work.weixin.qq.com/api/doc/90000/90135/90202) 
		- [ConvertToOpenid (/cgi-bin/user/convert_to_openid)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#ConvertToOpenid)
	- [openid转userid](https://work.weixin.qq.com/api/doc/90000/90135/90202) 
		- [ConvertToUserid (/cgi-bin/user/convert_to_userid)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#ConvertToUserid)
	- [二次验证](https://work.weixin.qq.com/api/doc/90000/90135/90203) 
		- [AuthSucc (/cgi-bin/user/authsucc)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#AuthSucc)
	- [邀请成员](https://work.weixin.qq.com/api/doc/90000/90135/90975) 
		- [BatchInvite (/cgi-bin/batch/invite)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#BatchInvite)
	- [获取加入企业二维码](https://work.weixin.qq.com/api/doc/90000/90135/91714) 
		- [GetJoinQrcode (/cgi-bin/corp/get_join_qrcode)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#GetJoinQrcode)
	- [获取企业活跃成员数](https://work.weixin.qq.com/api/doc/90000/90135/92714) 
		- [GetActiveStat (/cgi-bin/user/get_active_stat)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#GetActiveStat)
	- [创建部门](https://work.weixin.qq.com/api/doc/90000/90135/90205) 
		- [DepartmentCreate (/cgi-bin/department/create)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#DepartmentCreate)
	- [更新部门](https://work.weixin.qq.com/api/doc/90000/90135/90206) 
		- [DepartmentUpdate (/cgi-bin/department/update)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#DepartmentUpdate)
	- [删除部门](https://work.weixin.qq.com/api/doc/90000/90135/90207) 
		- [DepartmentDelete (/cgi-bin/department/delete)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#DepartmentDelete)
	- [获取部门列表](https://work.weixin.qq.com/api/doc/90000/90135/90208) 
		- [DepartmentList (/cgi-bin/department/list)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#DepartmentList)
	- [创建标签](https://work.weixin.qq.com/api/doc/90000/90135/90210) 
		- [TagCreate (/cgi-bin/tag/create)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#TagCreate)
	- [更新标签名字](https://work.weixin.qq.com/api/doc/90000/90135/90211) 
		- [TagUpdate (/cgi-bin/tag/update)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#TagUpdate)
	- [删除标签](https://work.weixin.qq.com/api/doc/90000/90135/90212) 
		- [TagDelete (/cgi-bin/tag/delete)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#TagDelete)
	- [获取标签成员](https://work.weixin.qq.com/api/doc/90000/90135/90213) 
		- [TagGet (/cgi-bin/tag/get)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#TagGet)
	- [增加标签成员](https://work.weixin.qq.com/api/doc/90000/90135/90214) 
		- [TagAddTagUsers (/cgi-bin/tag/addtagusers)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#TagAddTagUsers)
	- [删除标签成员](https://work.weixin.qq.com/api/doc/90000/90135/90215) 
		- [TagDelTagUsers (/cgi-bin/tag/deltagusers)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#TagDelTagUsers)
	- [获取标签列表](https://work.weixin.qq.com/api/doc/90000/90135/90216) 
		- [TagList (/cgi-bin/tag/list)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#TagList)
	- [增量更新成员](https://work.weixin.qq.com/api/doc/90000/90135/90980) 
		- [SyncUser (/cgi-bin/batch/syncuser)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#SyncUser)
	- [全量覆盖成员](https://work.weixin.qq.com/api/doc/90000/90135/90981) 
		- [ReplaceUser (/cgi-bin/batch/replaceuser)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#ReplaceUser)
	- [全量覆盖部门](https://work.weixin.qq.com/api/doc/90000/90135/90982) 
		- [ReplaceParty (/cgi-bin/batch/replaceparty)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#ReplaceParty)
	- [获取异步任务结果](https://work.weixin.qq.com/api/doc/90000/90135/90983) 
		- [JobGetResult (/cgi-bin/batch/getresult)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/contact?tab=doc#JobGetResult)
- 外部联系人管理(externalcontact)
	- [获取配置了客户联系功能的成员列表](https://work.weixin.qq.com/api/doc/90000/90135/92571) 
		- [GetFollowUserList (/cgi-bin/externalcontact/get_follow_user_list)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#GetFollowUserList)
	- [客户联系「联系我」管理](https://work.weixin.qq.com/api/doc/90000/90135/92572) 
		- [AddContactWay (/cgi-bin/externalcontact/add_contact_way)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#AddContactWay)
	- [客户联系「联系我」管理](https://work.weixin.qq.com/api/doc/90000/90135/92572) 
		- [GetContactWay (/cgi-bin/externalcontact/get_contact_way)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#GetContactWay)
	- [更新企业已配置的「联系我」方式](https://work.weixin.qq.com/api/doc/90000/90135/92572) 
		- [UpdateContactWay (/cgi-bin/externalcontact/update_contact_way)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#UpdateContactWay)
	- [客户联系「联系我」管理](https://work.weixin.qq.com/api/doc/90000/90135/92572) 
		- [DelContactWay (/cgi-bin/externalcontact/del_contact_way)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#DelContactWay)
	- [客户联系「联系我」管理](https://work.weixin.qq.com/api/doc/90000/90135/92572) 
		- [CloseTempChat (/cgi-bin/externalcontact/close_temp_chat)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#CloseTempChat)
	- [获取客户列表](https://work.weixin.qq.com/api/doc/90000/90135/92113) 
		- [List (/cgi-bin/externalcontact/list)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#List)
	- [获取客户详情](https://work.weixin.qq.com/api/doc/90000/90135/92114) 
		- [Get (/cgi-bin/externalcontact/get)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#Get)
	- [修改客户备注信息](https://work.weixin.qq.com/api/doc/90000/90135/92115) 
		- [Remark (/cgi-bin/externalcontact/remark)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#Remark)
	- [获取企业标签库](https://work.weixin.qq.com/api/doc/90000/90135/92117) 
		- [GetCorpTagList (/cgi-bin/externalcontact/get_corp_tag_list)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#GetCorpTagList)
	- [添加企业客户标签](https://work.weixin.qq.com/api/doc/90000/90135/92117) 
		- [AddCorpTag (/cgi-bin/externalcontact/add_corp_tag)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#AddCorpTag)
	- [编辑企业客户标签](https://work.weixin.qq.com/api/doc/90000/90135/92117) 
		- [EditCorpTag (/cgi-bin/externalcontact/edit_corp_tag)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#EditCorpTag)
	- [删除企业客户标签](https://work.weixin.qq.com/api/doc/90000/90135/92117) 
		- [DelCorpTag (/cgi-bin/externalcontact/del_corp_tag)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#DelCorpTag)
	- [编辑客户企业标签](https://work.weixin.qq.com/api/doc/90000/90135/92118) 
		- [MarkTag (/cgi-bin/externalcontact/mark_tag)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#MarkTag)
	- [获取客户群列表](https://work.weixin.qq.com/api/doc/90000/90135/92120) 
		- [GroupchatList (/cgi-bin/externalcontact/groupchat/list)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#GroupchatList)
	- [获取客户群详情](https://work.weixin.qq.com/api/doc/90000/90135/92122) 
		- [GroupchatGet (/cgi-bin/externalcontact/groupchat/get)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#GroupchatGet)
	- [添加企业群发消息任务](https://work.weixin.qq.com/api/doc/90000/90135/92135) 
		- [AddMsgTemplate (/cgi-bin/externalcontact/add_msg_template)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#AddMsgTemplate)
	- [获取企业群发消息发送结果](https://work.weixin.qq.com/api/doc/90000/90135/92136) 
		- [GetGroupMsgResult (/cgi-bin/externalcontact/get_group_msg_result)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#GetGroupMsgResult)
	- [发送新客户欢迎语](https://work.weixin.qq.com/api/doc/90000/90135/92137) 
		- [SendWelcomeMsg (/cgi-bin/externalcontact/send_welcome_msg)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#SendWelcomeMsg)
	- [添加群欢迎语素材](https://work.weixin.qq.com/api/doc/90000/90135/92366) 
		- [GroupWelcomeTemplateAdd (/cgi-bin/externalcontact/group_welcome_template/add)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#GroupWelcomeTemplateAdd)
	- [编辑群欢迎语素材](https://work.weixin.qq.com/api/doc/90000/90135/92366) 
		- [GroupWelcomeTemplateEdit (/cgi-bin/externalcontact/group_welcome_template/edit)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#GroupWelcomeTemplateEdit)
	- [获取群欢迎语素材](https://work.weixin.qq.com/api/doc/90000/90135/92366) 
		- [GroupWelcomeTemplateGet (/cgi-bin/externalcontact/group_welcome_template/get)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#GroupWelcomeTemplateGet)
	- [删除群欢迎语素材](https://work.weixin.qq.com/api/doc/90000/90135/92366) 
		- [GroupWelcomeTemplateDel (/cgi-bin/externalcontact/group_welcome_template/del)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#GroupWelcomeTemplateDel)
	- [获取离职成员的客户列表](https://work.weixin.qq.com/api/doc/90000/90135/92124) 
		- [GetUnassignedList (/cgi-bin/externalcontact/get_unassigned_list)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#GetUnassignedList)
	- [离职成员的外部联系人再分配](https://work.weixin.qq.com/api/doc/90000/90135/92125) 
		- [Transfer (/cgi-bin/externalcontact/transfer)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#Transfer)
	- [离职成员的群再分配](https://work.weixin.qq.com/api/doc/90000/90135/92127) 
		- [GroupchatTransfer (/cgi-bin/externalcontact/groupchat/transfer)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#GroupchatTransfer)
	- [获取联系客户统计数据](https://work.weixin.qq.com/api/doc/90000/90135/92132) 
		- [GetUserBehaviorData (/cgi-bin/externalcontact/get_user_behavior_data)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#GetUserBehaviorData)
	- [获取客户群统计数据](https://work.weixin.qq.com/api/doc/90000/90135/92133) 
		- [GroupchatStatistic (/cgi-bin/externalcontact/groupchat/statistic)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/externalcontact?tab=doc#GroupchatStatistic)
- 身份验证(oauth)
	- [构造网页授权链接](https://work.weixin.qq.com/api/doc/90000/90135/91022) 
		- [GetAuthorizeUrl (/connect/oauth2/authorize)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/oauth?tab=doc#GetAuthorizeUrl)
	- [获取访问用户身份](https://work.weixin.qq.com/api/doc/90000/90135/91023) 
		- [GetUserInfo (/cgi-bin/user/getuserinfo)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/oauth?tab=doc#GetUserInfo)
- 身份验证(verify)
	- [获取访问用户身份](https://work.weixin.qq.com/api/doc/90000/90135/91023) 
		- [GetUserInfo (/cgi-bin/user/getuserinfo)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/verify?tab=doc#GetUserInfo)
- 应用管理(app)
	- [获取应用](https://work.weixin.qq.com/api/doc/90000/90135/90227) 
		- [AgentGet (/cgi-bin/agent/get)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/app?tab=doc#AgentGet)
	- [获取应用](https://work.weixin.qq.com/api/doc/90000/90135/90227) 
		- [AgentList (/cgi-bin/agent/list)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/app?tab=doc#AgentList)
	- [设置应用](https://work.weixin.qq.com/api/doc/90000/90135/90228) 
		- [AgentSet (/cgi-bin/agent/set)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/app?tab=doc#AgentSet)
	- [创建菜单](https://work.weixin.qq.com/api/doc/90000/90135/90231) 
		- [MenuCreate (/cgi-bin/menu/create)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/app?tab=doc#MenuCreate)
	- [获取菜单](https://work.weixin.qq.com/api/doc/90000/90135/90232) 
		- [MenuGet (/cgi-bin/menu/get)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/app?tab=doc#MenuGet)
	- [删除菜单](https://work.weixin.qq.com/api/doc/90000/90135/90233) 
		- [MenuDelete (/cgi-bin/menu/delete)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/app?tab=doc#MenuDelete)
	- [设置工作台自定义展示](https://work.weixin.qq.com/api/doc/90000/90135/92535) 
		- [SetWorkbenchTemplate (/cgi-bin/agent/set_workbench_template)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/app?tab=doc#SetWorkbenchTemplate)
	- [设置工作台自定义展示](https://work.weixin.qq.com/api/doc/90000/90135/92535) 
		- [GetWorkbenchTemplate (/cgi-bin/agent/get_workbench_template)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/app?tab=doc#GetWorkbenchTemplate)
	- [设置工作台自定义展示](https://work.weixin.qq.com/api/doc/90000/90135/92535) 
		- [SetWorkbenchData (/cgi-bin/agent/set_workbench_data)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/app?tab=doc#SetWorkbenchData)
- 消息推送(message)
	- [发送应用消息](https://work.weixin.qq.com/api/doc/90000/90135/90236) 
		- [Send (/cgi-bin/message/send)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/message?tab=doc#Send)
	- [更新任务卡片消息状态](https://work.weixin.qq.com/api/doc/90000/90135/91579) 
		- [UpdateTaskcard (/cgi-bin/message/update_taskcard)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/message?tab=doc#UpdateTaskcard)
	- [创建群聊会话](https://work.weixin.qq.com/api/doc/90000/90135/90245) 
		- [AppchatCreate (/cgi-bin/appchat/create)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/message?tab=doc#AppchatCreate)
	- [修改群聊会话](https://work.weixin.qq.com/api/doc/90000/90135/90246) 
		- [AppchatUpdate (/cgi-bin/appchat/update)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/message?tab=doc#AppchatUpdate)
	- [获取群聊会话](https://work.weixin.qq.com/api/doc/90000/90135/90247) 
		- [AppchatGet (/cgi-bin/appchat/get)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/message?tab=doc#AppchatGet)
	- [应用推送消息](https://work.weixin.qq.com/api/doc/90000/90135/90248) 
		- [AppchatSend (/cgi-bin/appchat/send)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/message?tab=doc#AppchatSend)
	- [互联企业消息推送](https://work.weixin.qq.com/api/doc/90000/90135/90250) 
		- [LinkedcorpMessageSend (/cgi-bin/linkedcorp/message/send)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/message?tab=doc#LinkedcorpMessageSend)
	- [查询应用消息发送统计](https://work.weixin.qq.com/api/doc/90000/90135/92369) 
		- [GetStatistics (/cgi-bin/message/get_statistics)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/message?tab=doc#GetStatistics)
- 素材管理(material)
	- [上传临时素材](https://work.weixin.qq.com/api/doc/90000/90135/90253) 
		- [Upload (/cgi-bin/media/upload)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/material?tab=doc#Upload)
	- [上传图片](https://work.weixin.qq.com/api/doc/90000/90135/90256) 
		- [UploadImg (/cgi-bin/media/uploadimg)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/material?tab=doc#UploadImg)
	- [获取临时素材](https://work.weixin.qq.com/api/doc/90000/90135/90254) 
		- [Get (/cgi-bin/media/get)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/material?tab=doc#Get)
	- [获取高清语音素材](https://work.weixin.qq.com/api/doc/90000/90135/90255) 
		- [Jssdk (/cgi-bin/media/get/jssdk)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/material?tab=doc#Jssdk)
- OA(oa)
	- [获取打卡数据](https://work.weixin.qq.com/api/doc/90000/90135/90262) 
		- [GetCheckinData (/cgi-bin/checkin/getcheckindata)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/oa?tab=doc#GetCheckinData)
	- [获取打卡规则](https://work.weixin.qq.com/api/doc/90000/90135/90263) 
		- [GetCheckinPption (/cgi-bin/checkin/getcheckinoption)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/oa?tab=doc#GetCheckinPption)
	- [获取审批模板详情](https://work.weixin.qq.com/api/doc/90000/90135/91982) 
		- [GetTemplateDetail (/cgi-bin/oa/gettemplatedetail)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/oa?tab=doc#GetTemplateDetail)
	- [提交审批申请](https://work.weixin.qq.com/api/doc/90000/90135/91853) 
		- [ApplyEvent (/cgi-bin/oa/applyevent)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/oa?tab=doc#ApplyEvent)
	- [批量获取审批单号](https://work.weixin.qq.com/api/doc/90000/90135/91816) 
		- [GetApprovalInfo (/cgi-bin/oa/getapprovalinfo)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/oa?tab=doc#GetApprovalInfo)
	- [获取审批申请详情](https://work.weixin.qq.com/api/doc/90000/90135/91983) 
		- [GetApprovalDetail (/cgi-bin/oa/getapprovaldetail)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/oa?tab=doc#GetApprovalDetail)
	- [获取审批数据（旧）](https://work.weixin.qq.com/api/doc/90000/90135/91530) 
		- [GetApprovalData (/cgi-bin/corp/getapprovaldata)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/oa?tab=doc#GetApprovalData)
	- [获取公费电话拨打记录](https://work.weixin.qq.com/api/doc/90000/90135/90267) 
		- [GetDialRecord (/cgi-bin/dial/get_dial_record)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/oa?tab=doc#GetDialRecord)
	- [查询自建应用审批单当前状态](https://work.weixin.qq.com/api/doc/90000/90135/90269) 
		- [GetOpenApprovalData (/cgi-bin/corp/getopenapprovaldata)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/oa?tab=doc#GetOpenApprovalData)
- 日程(calendar)
	- [创建日历](https://work.weixin.qq.com/api/doc/90000/90135/92618) 
		- [CalendarAdd (/cgi-bin/oa/calendar/add)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/calendar?tab=doc#CalendarAdd)
	- [更新日历](https://work.weixin.qq.com/api/doc/90000/90135/92619) 
		- [CalendarUpdate (/cgi-bin/oa/calendar/update)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/calendar?tab=doc#CalendarUpdate)
	- [获取日历](https://work.weixin.qq.com/api/doc/90000/90135/92621) 
		- [CalendarGet (/cgi-bin/oa/calendar/get)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/calendar?tab=doc#CalendarGet)
	- [删除日历](https://work.weixin.qq.com/api/doc/90000/90135/92620) 
		- [CalendarDel (/cgi-bin/oa/calendar/del)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/calendar?tab=doc#CalendarDel)
	- [创建日程](https://work.weixin.qq.com/api/doc/90000/90135/92622) 
		- [ScheduleAdd (/cgi-bin/oa/schedule/add)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/calendar?tab=doc#ScheduleAdd)
	- [更新日程](https://work.weixin.qq.com/api/doc/90000/90135/92623) 
		- [ScheduleUpdate (/cgi-bin/oa/schedule/update)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/calendar?tab=doc#ScheduleUpdate)
	- [获取日程](https://work.weixin.qq.com/api/doc/90000/90135/92624) 
		- [ScheduleGet (/cgi-bin/oa/schedule/get)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/calendar?tab=doc#ScheduleGet)
	- [取消日程](https://work.weixin.qq.com/api/doc/90000/90135/92625) 
		- [ScheduleDel (/cgi-bin/oa/schedule/del)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/calendar?tab=doc#ScheduleDel)
	- [获取日历下的日程列表](https://work.weixin.qq.com/api/doc/90000/90135/92626) 
		- [ScheduleGetByCalendar (/cgi-bin/oa/schedule/get_by_calendar)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/calendar?tab=doc#ScheduleGetByCalendar)
- 会议室(meetingroom)
	- [添加会议室](https://work.weixin.qq.com/api/doc/90000/90135/92793) 
		- [Add (/cgi-bin/oa/meetingroom/add)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/meetingroom?tab=doc#Add)
	- [查询会议室](https://work.weixin.qq.com/api/doc/90000/90135/92793) 
		- [List (/cgi-bin/oa/meetingroom/list)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/meetingroom?tab=doc#List)
	- [编辑会议室](https://work.weixin.qq.com/api/doc/90000/90135/92793) 
		- [Edit (/cgi-bin/oa/meetingroom/edit)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/meetingroom?tab=doc#Edit)
	- [删除会议室](https://work.weixin.qq.com/api/doc/90000/90135/92793) 
		- [Del (/cgi-bin/oa/meetingroom/del)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/meetingroom?tab=doc#Del)
	- [查询会议室的预定信息](https://work.weixin.qq.com/api/doc/90000/90135/92794) 
		- [GetBookingInfo (/cgi-bin/oa/meetingroom/get_booking_info)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/meetingroom?tab=doc#GetBookingInfo)
	- [预定会议室](https://work.weixin.qq.com/api/doc/90000/90135/92794) 
		- [Book (/cgi-bin/oa/meetingroom/book)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/meetingroom?tab=doc#Book)
	- [取消预定会议室](https://work.weixin.qq.com/api/doc/90000/90135/92794) 
		- [CancelBook (/cgi-bin/oa/meetingroom/cancel_book)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/meetingroom?tab=doc#CancelBook)
- 企业支付(pay)
- 电子发票(invoice)
	- [查询电子发票](https://work.weixin.qq.com/api/doc/90000/90135/90284) 
		- [GetInvoiceInfo (/cgi-bin/card/invoice/reimburse/getinvoiceinfo)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/invoice?tab=doc#GetInvoiceInfo)
	- [更新发票状态](https://work.weixin.qq.com/api/doc/90000/90135/90285) 
		- [UpdateInvoiceStatus (/cgi-bin/card/invoice/reimburse/updateinvoicestatus)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/invoice?tab=doc#UpdateInvoiceStatus)
	- [批量更新发票状态](https://work.weixin.qq.com/api/doc/90000/90135/90286) 
		- [UpdateStatusBatch (/cgi-bin/card/invoice/reimburse/updatestatusbatch)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/invoice?tab=doc#UpdateStatusBatch)
	- [批量查询电子发票](https://work.weixin.qq.com/api/doc/90000/90135/90287) 
		- [GetInvoiceInfoBatch (/cgi-bin/card/invoice/reimburse/getinvoiceinfobatch)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/invoice?tab=doc#GetInvoiceInfoBatch)
- 会话内容存档(msgaudit)
	- [获取会话内容](https://work.weixin.qq.com/api/doc/90000/90135/91774) 
		- [GetRobotInfo (/cgi-bin/msgaudit/get_robot_info)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/msgaudit?tab=doc#GetRobotInfo)
	- [获取会话内容存档开启成员列表](https://work.weixin.qq.com/api/doc/90000/90135/91614) 
		- [GetPermitUserList (/cgi-bin/msgaudit/get_permit_user_list)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/msgaudit?tab=doc#GetPermitUserList)
	- [获取会话内容存档内部群信息](https://work.weixin.qq.com/api/doc/90000/90135/92951) 
		- [GroupchatGet (/cgi-bin/msgaudit/groupchat/get)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/msgaudit?tab=doc#GroupchatGet)
- 企业直播(living)
	- [获取成员直播ID列表](https://work.weixin.qq.com/api/doc/90000/90135/92735) 
		- [GetUserLivingid (/cgi-bin/living/get_user_livingid)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/living?tab=doc#GetUserLivingid)
	- [获取直播详情](https://work.weixin.qq.com/api/doc/90000/90135/92734) 
		- [GetLivingInfo (/cgi-bin/living/get_living_info)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/living?tab=doc#GetLivingInfo)
	- [获取看直播统计](https://work.weixin.qq.com/api/doc/90000/90135/92736) 
		- [GetWatchStat (/cgi-bin/living/get_watch_stat)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/living?tab=doc#GetWatchStat)
- 健康上报(health)
	- [获取健康上报使用统计](https://work.weixin.qq.com/api/doc/90000/90135/92747) 
		- [GetHealthReportStat (/cgi-bin/health/get_health_report_stat)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/health?tab=doc#GetHealthReportStat)
	- [获取健康上报任务ID列表](https://work.weixin.qq.com/api/doc/90000/90135/92749) 
		- [GetReportJobids (/cgi-bin/health/get_report_jobids)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/health?tab=doc#GetReportJobids)
	- [获取健康上报任务详情](https://work.weixin.qq.com/api/doc/90000/90135/92751) 
		- [GetReportJobInfo (/cgi-bin/health/get_report_job_info)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/health?tab=doc#GetReportJobInfo)
	- [获取用户填写答案](https://work.weixin.qq.com/api/doc/90000/90135/92754) 
		- [GetReportAnswer (/cgi-bin/health/get_report_answer)](https://pkg.go.dev/github.com/fastwego/wxwork/corporation/apis/health?tab=doc#GetReportAnswer)
