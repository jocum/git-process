# git 版本管理基础流程     

# 先来个简易流程图  
  ![image](https://github.com/jocum/git-process/blob/master/img/process.png)
  
  
  # 结构
      1. master (版本 1.0.0  1.0.1  等等也是类似master 的存在 纯代码库)
          首先我们有一个简单的结构  有一个代码分支 master 这个是纯代码分支没有实际成项目 最标准的代码库,
          然后在开发过程中可能会产生一个一个版本 例如 版本1.0.0  可以创建独立的分支保留其版本 类似master 的枝丫.
      2. online 
          online 是生成环境代码分支,即用online 这个分支的代码运行起来形成一个服务.也就是项目的线上运行代码
      3. dev
          dev 是测试分支,用测试环境跑该套代码 所有开发中的程序,bug 提交 都在该环境测试
         (注:如果是业务更加保险可以做个预上线分支 就是 在dev 和online 之间还有一个测试环境 预上线环境 这里不做讨论)
   # 流程
      1. 以上图为例 你需要开发一个pay 功能 那么 切换到本地master 获取最新的origin/master 的代码 ,
          然后创建本地开发分支pay
          (注: 如果pay这个功能需要多人协助 可以将pay 这个分支推送到远端 生成origin/pay 然后多人提交代码通过origin/pay 同步交流)
       2. pay 分支开发完成形成提交commit01、commit02 ... commit07,  合并分支到dev 进行测试
       
       3. dev测试有bug 则回到pay分支修改bug,产生commit-bug01、commit-bug02... commit-bug10086. 最终测试通过 完成pay功能
       (可喜可贺 可喜可贺).
       
       4. 整理pay分支 将所有的提交 commit01~commitbug10086  通过 git reset hash(该hash 是commit01 产生前的一个hash ),这个命令会重置 从commit01开始往后
            的所有提交 成未提交状态,然后重新commit  产生commit-pay 完成本次开发
            
       5. 将本次任务commit-pay  合并到online 分支进行上线部署, 线上运行ok . 合并online 分支到master 保证master 分支是最新的代码.
            从master 分支创建一个预留分支 pay  方便后期出现线上bug 回滚代码
       
       6.如果线上运行有bug  则返回pay 分支处理 所有pay 分支可以保留一段时间 如果时间太长可以删除
       
       (注1: 由于dev 分支在多次沉余,和有可能放弃的提交都在dev分支 merge 可能有点艰难 可以选择用 cherry-pick 这个命令 缺点是提交只能根据hash一次一次提交)
       (注2: 由于dev分支的偏差 可以定期删除dev 分支 从master 重新生成dev 保证dev 偏离在一点范围内)
       (注3: 有问题到时候在讨论修改流程, 共勉)
   
