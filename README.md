# nilshinn
template <typename R, typename ... T>
void ssss(std::function<R(T ...)> f, T ... t)
{
  std::cout << f(t...) << std::endl;
  std::cout << f(std::forward<T>(t)...) << std::endl;
}
ssss<int, int, int>(std::function<int(int,int)>{add}, 1, 2);

  template <typename R, typename... A>
  R decorate(std::function<R(A...)> f, A... a)
  {
    static std::map<uintptr_t, unsigned int> _map;
    auto key = reinterpret_cast<uintptr_t>(f.template target<R(*)(A...)>());
    if (_map.find(key) == _map.end()) _map[key] = 0;
    else ++_map[key];
    #ifdef _debug_
    std::cout << "enter decorate:" << std::endl;
    std::cout << "D " << key << ":" << _map[key] << std::endl;
    #endif
    auto r = f(std::forward<A>(a)...);
    #ifdef _debug_
    std::cout << "exit decorate:" << std::endl;
    #endif
    return r;
  }
