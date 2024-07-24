# 1.About Bantian

It is small coffee yard, located in FuYang Bashan village, operated by a couple with art background.
Try to name it for the high school friendship ideas.

# 2.Idea-1: 班级基金
为了方便搞一些活动，提供一些经费支持，特别是像20周年之类的活动。
## 2.1.匿名、自愿、可追溯
a.目的: 捐多少纯属自愿，没有对比，捐赠记录公开可查

b.规则: 每人有一个固定的ID(`sha256("<姓名首字母缩写>"+"<\$salt>"`)后得到的前8个字节)，其中\$salt是用户自己提供的任意一段字符， 比如身份证后4位之类的。
比如: 汤忠忠, 提供的$salt是 "1234"，那么对应 `sha256(tzz1234)[:8]`, 结果为: "69abd3fd1d0d2f4b"
```
// try it:  https://go.dev/play/p/HR3o4T6UGEP
package main

import (
	"crypto/sha256"
	"fmt"
)

func main() {
	sum := sha256.Sum256([]byte("tzz1234"))
	fmt.Printf("%x\n", sum[:8])
}
```
## 2.2.相关角色
- 捐赠者: everyone
- 管理员: admin, 接受并公开捐赠信息，提供资金，并公开账单
- 资金审核委员: auditors, 决定是否支持某项活动支出

其中admin, auditors的信息是公开的

## 2.3.最大限额(10W)、资金托管
不希望资金池太大，一旦余额>=10w, 就不再接受捐赠, 大额资金管理难度太大
简单起见，不考虑资金的收益，即假设资金只保本，不产生任何收益。(admin可以根据情况发红包...)

## 2.4.资金使用条件
- 所有有老师参与的活动?
- 其他"资金审核委员" 同意的项目, [50%, 100%]的投票赞成, 比如委员会4个人，只要2人同意即可
- 鼓励资金有效利用，鼓励做些有意义的事情

## 2.5.操作流程
- 捐赠者私下捐给 admin
- admin 根据用户ID，更新捐赠记录
- 举行活动前, 如需使用资金，最好先获得委员会的投票；事后也可以，但有不通过的风险
- 提供费用清单，先垫付 or admin 直接支付都可以
- admin 更新账单信息

## 2.6.FAQ
- Q1: 私下捐给admin是否也保留了捐款人信息?
- A1: Yes, admin需要保密，没有太严格的要求, 一旦泄漏了也没事，捐赠者后续也可以修改salt;

- Q2: 忘记了自己的salt?
- A2: 如果大家都不记得了，那就真的匿名了，无迹可查

- Q3: 账单在哪里公开?
- A3: 在github(国内gitee), 每次修改都是有记录可查的, 可以借机了解一点点编程


