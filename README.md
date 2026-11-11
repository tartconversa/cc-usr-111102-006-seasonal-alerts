# 新商户冷启动的时序异常告警回放

本项目保存百货多业态经营研究的合成资料及输入读取工具。当前程序只解析文件并显示输入类型与记录数量，不进行统计分析、模型训练、优化求解或业务推荐。所有记录均为虚构，不能用于陈述真实商场经营结果。

## 输入约定

series 的空 amount 是开店缺测，数值0是已报告零。calendar 明示商户时段营业状态。events 与 labels 分别给 occurred_at、known_at，不应混为同一时间。

fixtures 为资料目录，src/series_reader.py 为读取器，tests 为格式读取测试。输入在运行中保持不变；研究计算结果可写入独立的 .workspace-output 目录。

## 本地操作

Python 3.11 及以上版本，现有读取工具只依赖标准库，不需要下载第三方包。进入项目根目录：

    python -m src.series_reader fixtures/series.csv

编译检查：

    python -m compileall -q src tests

格式读取测试：

    python -m unittest discover -s tests -v

## 固定运行环境

    docker build -t seasonal-alerts:local .
    docker run --rm seasonal-alerts:local

容器默认运行输入测试。镜像使用完整内容摘要固定，研究输入随项目一起复制。
