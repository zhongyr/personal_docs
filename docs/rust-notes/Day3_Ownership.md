# Ownership

我们先用C代码看一下ownership的概念，和在C中遇到的问题。

```C
/* 
 * Open vSwitch
 * Get status of the virtual prot. The caller is responsible for freeing '*errp' (with free()).
*/ 
int (*vport_get_status)(const struct ofport *port, char **errp);
```

这个其实就是一个转交ownership在C的体现，函数拥有errp的ownership，然后函数把ownership给到了caller。

```C
/**
 * ffmpeg
 * @note Any old dictionary present is discarded and replaced with a copy of the new one. The 
 * caller still owns val is and responsible for freeing it.
*/

int av_opt_set_dict_val(void *obj, const char *name, const AVDictionary *val, int search_flags);
```
这段代码是borrow的一个体现，对于``AVDictionary *val``函数只是borrow了引用，并不是转交了ownership，内存管理还是由caller负责。

在C中，这种ownership的移交都是在注释中体现的，由于每个库都有可能实现自身特有的资源释放函数，而不是简单的调用free()，
所以使得在C中对于内存的管理变得十分复杂。例如在结构体中有多个指针，那么就有多个内存需要释放。

```C
/* Open vSwitch
 * The caller owns the data in 'port' and must free it with
 * ofproto_port_destory() when it is no longer needed. */

 int (*port_query_by_name)(const struct ofproto *ofproto,
                           const char *devname, struct ofproto_port *port);
```

但这种情况在Rust中就变得非常方便，因为ownership标记了caller的scope保留了ownership，所以在scope结束时，rust会释放这些资源。

```C
/**
 * @note this function doesn't frees the memory allocated by the demod,
 * by the SEC driver and by the tuner. In order to free it, an explicit call to 
 * dvb_frontend_detach() is needed, after calling this function.
 */
 int dvb_unregister_frontend(struct dvb_frontend *fe);
```

这是Linux Kernel中结构体内资源管理的一个例子，需要额外调用函数释放结构体中的资源。而在rust中，编译器会要求提前声明清楚资源的ownership来保证
资源能够在合适的时机被释放。

##　Compile time vs run time

在rust中，所有的这种ownership的管理都是要求在编译时确定的，用以保证运行时的正确。

rust在运行时的操作和C大致相同
* Passing ownership: passes a pointer
  compiler will insert the appropriate free() call
* Passing reference: passes a pointer
* Passing value: copy
