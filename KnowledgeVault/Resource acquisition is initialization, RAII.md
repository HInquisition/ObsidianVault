#Memory 
# Resource acquisition is initialization, RAII
**`Resource acquisition is initialization, Получение ресурсов есть инициализация`** - один из [[Software design patterns (Паттерны проектирования) | Паттернов проектирования]], суть которого заключается в создании связи между конструктором (деструктором) и выделением ресурсов (блокировка файлов, выделение памяти, сокеты и т.д.). Такой подход позволяет избежать ситуации, когда программист забывает освободить ресурс, ведь он освобождается автоматически. Важная часть паттерна -  [[Encapsulation (Инкапсуляция) |инкапсуляция]] управления ресурсами в локальном объекте, который находится в области видимости (функции например) и который будет уничтожен после выхода из нее, вместе с этим освободив ресурсы. 

Особенно полезно для языков и систем, не поддерживающих  [[Garbage Collector]].
Также позволяет избежать случаев, когда ресурсы не освобождаются из-за генерации исключений, так как деструктор локальных объектов вызывается независимо от причины выхода из функции.

Примерами использования паттерна являются умные указатели [[C++]], соответственно и умные указатели [[Unreal Engine]].

Другой пример - **`std::string`**  и **`std::vector`**

RAII can be used as an alternative to **`new`** and **`delete`** to make an object live independently of its scope. Such a technique consists of taking the pointer to the object that was allocated on the [[Memory Heap (Куча) |heap]] and placing it in a _handle/manager object_. The latter has a destructor that will take care of destroying the object. This will guarantee that the object is available to any function that wants access to it, and that the object is destroyed when the lifetime of the _handle object_ ends, without the need for explicit cleanup.
```cpp
void fn(const std::string& str)
{
    std::vector<char> vec;
    for (auto c : str)
        vec.push_back(c);
    // do something
}
```

when you create a vector and you push elements to it, you don't care about allocating and deallocating such elements. The vector uses **`new`** to allocate space for its elements on the heap, and **`delete`** to free that space. You as a user of vector you don't care about the implementation details and will trust vector not to leak. In this case, the vector is the _handle object_ of its elements. 
Источник - https://stackoverflow.com/questions/2321511/what-is-meant-by-resource-acquisition-is-initialization-raii

https://en.wikipedia.org/wiki/Resource_acquisition_is_initialization