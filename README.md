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

// filter
class Filter {
// using tmft = typename std::mem_fn<bool(int,int), Filter>;
// typedef typename std::mem_fn<bool(int,int), Filter> tmft;
typedef bool(Filter::*mft)(int, int);
std::map<std::string, mft>* _map;
public:
  Filter() {
    _map = new std::map<std::string, mft> {
     {"first", &Filter::_check1},
    };
  }
  bool filter(int info, int data) {
    std::cout << "ff1\n";
    for (auto it = _map->begin(); it != _map->end(); ++it) {
      auto r = (this->*it->second)(info, data);
      std::cout << "ff2\n";
      if (!r) return false;
    }
    for (const auto& it : c_map) {
      it.second(this, info, data);
    }
    return true;
  }
  bool _check1(int info, int data) {
    return true;
  }
const std::map<std::string, decltype(std::mem_fn(&Filter::filter))> c_map = {
{"first", std::mem_fn(&Filter::_check1)},
};
};
class Filter {
// using tmft = typename std::mem_fn<bool(int,int), Filter>;
// typedef typename std::mem_fn<bool(int,int), Filter> tmft;
typedef bool(Filter::*mft)(int, int);
std::map<std::string, mft>* _map;
public:
  Filter() {
    _map = new std::map<std::string, mft> {
     {"first", &Filter::_check1},
    };
  }
  bool filter(int info, int data) {
    std::cout << "ff1\n";
    for (auto it = _map->begin(); it != _map->end(); ++it) {
      auto r = (this->*it->second)(info, data);
      std::cout << "ff2\n";
      if (!r) return false;
    }
    for (const auto& it : c_map) {
      it.second(this, info, data);
    }
    return true;
  }
  bool _check1(int info, int data) {
    return true;
  }
const std::map<std::string, decltype(std::mem_fn(&Filter::filter))> c_map = {
{"first", std::mem_fn(&Filter::_check1)},
};
};
