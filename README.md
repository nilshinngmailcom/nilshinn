# nilshinn
template <typename R, typename ... T>
void ssss(std::function<R(T ...)> f, T ... t)
{
  std::cout << f(t...) << std::endl;
  std::cout << f(std::forward<T>(t)...) << std::endl;
}
ssss<int, int, int>(std::function<int(int,int)>{add}, 1, 2);
