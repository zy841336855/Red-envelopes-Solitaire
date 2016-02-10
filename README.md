# Red-envelopes-Solitaire
##背景
	现在在微信或者QQ上流行着一种红包接龙的游戏，对此游戏进行各种模拟个人收入并分析游
	戏公平性。
##游戏规则
- 每个红包内塞入一定金额的钱，只能分给特定个人数的人
- 红包先抢先得，抢到的人分的一定的随机金额(所有人的总净额为塞入的钱)
- 抢到红包的内金额最大的发下一个红包，形成接龙

##红包类实现

```cpp
class Packet
{
private:
    double Money;
    int Quota;
public:
    Packet(double  M,int Q);
    void SendPacket(int M,int Q);
    double GetMoney();
    double GetPrecent();
};
Packet::Packet(double M,int Q)
{
    Money=M;
    Quota=Q;
    srand((unsigned)time(NULL));
}
void Packet::SendPacket(int M,int Q)
{
    Money=M;
    Quota=Q;
    srand((unsigned)time(NULL));
}
double Packet::GetMoney()
{
    double Ans=0;
    if(Quota<=0)
        return Ans;
    if(Quota==1)
    {
        Quota--;
        Ans=Money;
        Money-=Ans;
        return Ans;
    }
    double Max=Money/Quota*2;
    double Min=0.01;
    Ans=Max*GetPrecent();
    Ans=((double)((int)(Ans*100)))/100;
    Ans=max(Ans,Min);
    Money-=Ans;
    Quota--;
    return Ans;
}
double Packet::GetPrecent()
{
    int Max=10000;
    int Rand=(unsigned)rand();
    Rand=Rand%Max;
    return (double)Rand/Max;
}

```
基本借鉴[程鹏的回答](http://www.zhihu.com/question/22625187)

##情形分析
###情形一
|红包获得情形|个人策略|环境|
|----------|-------|---|
|有抢必得|强取红包|与个人策略相同|


	
	
