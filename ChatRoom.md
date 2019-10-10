#  MiniProgram

## 1. 通用接口
### 1.1. 版本检查
1.1.1. 协议: C2S_CheckVersion  
1.1.2. 参数：版本号,例 1.0.1  
1.1.3. 返回协议:S2C_CheckVersion  
1.1.4. 返回参数:  
*{ErrorCode:0}*  
*{ErrorCode:1,ErrorDes:'Error Version'}* 
>说明：连接成功的第一步必须检查版本，不检查通过其他协议都不会响应

### 1.2. 用户身份
1.2.1. 协议: C2S_UserInfo  
1.2.2. 参数：{UId,Name,RoleName}  
1.2.3. 返回协议:S2C_UserInfo  
1.2.4. 返回参数: 无  
>说明：  
>UId 是用户唯一身份标识,不允许重复  
>Name 用于显示的用户名称  
>RoleName 用户角色,下面列表中的一个  
>+ LiveManager  直播房间管理员  
>+ LiveAnchor   直播房间主播  
>+ LiveAudience 直播房间用户  
>+ RollManager  娃娃机房间管理员  
>+ RollCamera   娃娃机房间摄像机  
>+ RollUser     娃娃机房间用户  

## 2. Live
### 2.1. 创建房间
2.1.1. 协议: C2S_CreateRoom  
2.1.2. 参数：无  
2.1.3. 返回协议:S2C_CreateRoom  
2.1.4. 返回参数:  
*{ErrorCode:0,RoomId}*  
*{ErrorCode:1,ErrorDes:'Manager Already In Room ' + RoomId}*
>说明：
>该协议限制仅为管理员可用 ,创建房间后管理员拥有以下权限：  
>>退出房间  
>>发送订单  
>>踢出用户  

### 2.2. 退出房间
2.2.1. 协议: C2S_ExitRoom  
2.2.2. 参数：无  
2.2.3. 返回协议:S2C_ExitRoom  
2.2.4. 返回参数:  
*{ErrorCode:0}*  
*{ErrorCode:1,ErrorDes:'Manager Not In Room.'}*

### 2.3. 发送订单
2.3.1. 协议: C2S_SendOrder  
2.3.2. 参数：订单数据  
2.3.3. 返回协议:S2C_SendOrder  
2.3.4. 返回参数:无
>说明：  
>该协议限制仅为管理员可用

### 2.4. 踢出用户
2.4.1. 协议: C2S_KickUser  
2.4.2. 参数：UserId  
2.4.3. 返回协议:S2C_KickUser  
2.4.4. 返回参数:
*{ErrorCode:0}*  
*{ErrorCode:1,ErrorDes:'Manager Not In Room.'}*  
*{ErrorCode:2,ErrorDes:'User ${data} Not In Room.'}*  
>说明：  
>该协议限制仅为管理员可用

### 2.5. 进入房间
2.5.1. 协议: C2S_EnterRoom  
2.5.2. 参数：RoomId  
2.5.3. 返回协议:S2C_EnterRoom  
2.5.4. 返回参数:  
*{ErrorCode:0,UserList:_UserList}*  
*{ErrorCode:1,ErrorDes:'Room ' + _RoomId + ' Not Exist.'}*   
*{ErrorCode:2,ErrorDes:'Already In Room ' + this.RoomId });*  
>说明：  
>该协议限制仅为主播、用户可用

### 2.6. 发送消息
2.6.1. 协议: C2S_SendMsg  
2.6.2. 参数：Msg  
2.6.3. 返回协议:无  
2.6.4. 返回参数:  

### 2.10. 广播解散房间
2.10.1. 协议: 无  
2.10.2. 参数：无  
2.10.3. 返回协议: BC_DismissRoom   
2.10.4. 返回参数:  

### 2.11. 广播订单信息
2.11.1. 协议: 无  
2.11.2. 参数：无  
2.11.3. 返回协议: BC_SendOrder  
2.11.4. 返回参数:转发房间管理员发送订单信息，结构由管理员开发确定

### 2.12. 广播进入房间
2.12.1. 协议: 无  
2.12.2. 参数：无  
2.12.3. 返回协议: BC_EnterRoom   
2.12.4. 返回参数: {UId,Name,RoleName}

### 2.13. 广播发送消息
2.10.1. 协议: 无  
2.10.2. 参数：无  
2.10.3. 返回协议:BC_SendMsg   
2.10.4. 返回参数: 转发客户端发送的系统消息，结构由主播和用户开发确定

## 2.Live

