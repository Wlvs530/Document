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
>+ RollMachine  娃娃机机器(此协议不可用)

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
*{ErrorCode:2,ErrorDes:'No User In Room ' + this.RoomId}*  
*{ErrorCode:3,ErrorDes:'User Not In Room ' + this.RoomId}*  

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


### 2.7. 操作娃娃机
2.6.1. 协议: C2S_Operate  
2.6.2. 参数：操作指令 
2.6.3. 返回协议:S2C_Operate  
2.6.4. 返回参数:  

### 2.10. 广播解散房间
2.10.1. 协议: 无  
2.10.2. 参数：无  
2.10.3. 返回协议: BC_DismissRoom   
2.10.4. 返回参数:  
*{ErrorCode:0}*  
*{ErrorCode:1,ErrorDes:'User Not In Room.'}*  
>操作指令:前端要响应按下和释放的指令
>BeginLeft
>StopLeft
>BeginRight
>StopRight
>BeginFront
>StopFront
>BeginBack
>StopBack
>Catch

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

## 3.Doll
### 3.1. 创建房间
3.1.1. 协议: C2S_CreateRoom  
3.1.2. 参数：娃娃机机器名
3.1.3. 返回协议:S2C_CreateRoom  
3.1.4. 返回参数:  
*{ErrorCode:0,RoomId}*  
*{ErrorCode:1,ErrorDes:'Manager Already In Room ' + RoomId}*  
*{ErrorCode:2,ErrorDes:`Machine ${data} Not Exist` }*
>说明：
>该协议限制仅为管理员可用 ,创建房间后管理员拥有以下权限：  
>>退出房间  
>>指定为操作者 

### 3.2. 退出房间
3.2.1. 协议: C2S_ExitRoom  
3.2.2. 参数：无  
3.2.3. 返回协议:S2C_ExitRoom  
3.2.4. 返回参数:  
*{ErrorCode:0}*  
*{ErrorCode:1,ErrorDes:'Manager Not In Room.'}*  
*{ErrorCode:2,ErrorDes:'No User In Room ' + this.RoomId}*  
*{ErrorCode:3,ErrorDes:'User Not In Room ' + this.RoomId}*  

### 3.3. 指定为操作者
3.3.1. 协议: C2S_ChangeToOperator  
3.3.2. 参数：UId   
3.3.3. 返回协议:S2C_ChangeToOperator  
3.3.4. 返回参数:  
*{ErrorCode:0}*  
*{ErrorCode:1,ErrorDes:'Manager Not In Room'}*  
*{ErrorCode:2,ErrorDes:'User ' + this.Room.Operator.UId + ' Is Operating'}*  
*{ErrorCode:3,ErrorDes:'User ' + data.UId + ' Not In Room'}*  
>说明：
>该协议限制仅为管理员可用 ,指定操作者后管理员拥有以下权限：  
>>开始游戏  
>>指定为用户

### 3.4. 指定为用户
3.4.1. 协议: C2S_ChangeToUser  
3.4.2. 参数：无   
3.4.3. 返回协议:S2C_ChangeToOperator  
3.4.4. 返回参数:  
*{ErrorCode:0}*  
*{ErrorCode:1,ErrorDes:'Manager Not In Room'}*  
*{ErrorCode:2,ErrorDes:'Operator Is Not Exist.'}*  
>说明：
>该协议限制仅为管理员可用

### 3.5. 开始游戏
3.5.1. 协议: C2S_BeginGame  
3.5.2. 参数：   
3.5.3. 返回协议:S2C_BeginGame  
3.5.4. 返回参数:  
无
*{ErrorCode:0}*  
*{ErrorCode:1,ErrorDes:'Manager Not In Room'}*  
*{ErrorCode:2,ErrorDes:'Machine Not In Room'}*  
*{ErrorCode:3,ErrorDes:'Operator Not In Room'}*  
>说明：
>该协议限制仅为管理员可用
>S2C_BeginGame 返回协议会同步通知操作者，所以用户必须响应
>在用户侧，这个返回协议没有返回参数

### 3.6. 进入房间
3.6.1. 协议: C2S_EnterRoom  
3.6.2. 参数：RoomId  
3.6.3. 返回协议:S2C_EnterRoom  
3.6.4. 返回参数:  
*{ErrorCode:0,UserList:_UserList}*  
*{ErrorCode:1,ErrorDes:'Room ' + _RoomId + ' Not Exist.'}*  
*{ErrorCode:2,ErrorDes:'Already In Room ' + this.Room.RoomId }*  

### 3.10. 广播解散房间
3.10.1. 协议: 无  
3.10.2. 参数：无  
3.10.3. 返回协议: BC_DismissRoom   
3.10.4. 返回参数: 

### 3.11. 广播进入房间
3.11.1. 协议: 无  
3.11.2. 参数：无  
3.11.3. 返回协议: BC_EnterRoom   
3.11.4. 返回参数: {UId,Name,RoleName}
>备注：如果RoleName == RollMachine , 则没有UId

### 3.12. 广播退出房间
3.12.1. 协议: 无  
3.12.2. 参数：无  
3.12.3. 返回协议: BC_ExitRoom   
3.12.4. 返回参数: {UId,RoleName}
>备注：如果RoleName == RollMachine , 则没有UId

### 3.13. 广播指定成操作者
3.13.1. 协议: 无  
3.13.2. 参数：无  
3.13.3. 返回协议: BC_ChangeToOperator   
3.13.4. 返回参数: UId

### 3.14. 广播指定成用户
3.14.1. 协议: 无  
3.14.2. 参数：无  
3.14.3. 返回协议: BC_ChangeToUser   
3.14.4. 返回参数: UId

### 3.14. 广播游戏结束
3.14.1. 协议: 无  
3.14.2. 参数：无  
3.14.3. 返回协议: BC_GameOver   
3.14.4. 返回参数: Gain
> Gain == 0 没有抓到礼品
> Gain == 1 抓到礼品