# yy-deliver-coding

## Coding ✍️

#### Livewireコンポーネントの利用
Livewireコンポーネントを呼び出す場合、書き方は1つに統一しましょう。

**Bad**
```PHP
<livewire:some-component />
```

**Good**
```PHP
@livewire('some-component')
```


#### Livewire内でのモデルの取得/生成
コンポーネント単位で提供される非同期の処理をアクションと呼び出し、 `App\Actions` 直下にまとめましょう。

**Bad**

```PHP
namespace App\Http\Livewire;

use Livewire\Component;
use App\Models\Flight;

$flight = Flight::create($input);
```

**Good**
```PHP
namespace App\Http\Livewire;

use App\Actions\CreateFlight;

return app(CreateFlight::class)->create($input);
```


```PHP
namespace App\Actions;

use App\Contracts\Actions\CreateFlights;
use App\Models\Flight;

class CreateFlight implements CreateFlights
{
    public function create(array $input)
    {
        Validator::make($input, [
          // Do something...
        ])->validate();

        return Flight::create($input);
    }
}
```


```PHP
namespace App\Contracts\Actions;

interface CreateFlights
{
    public function create(array $input);
}
```
