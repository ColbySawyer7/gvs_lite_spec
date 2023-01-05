# GVS Development Specification

## Object-Oriented Approach

### Generic Objects Examples

<details>
    <summary> Virtual Machine Class </summary>

    class VM{
        int id,
        required int cores,
                int[] specific_cores = [0*cores],
        required int memory,
        required int disk_gb,
                String os = 'Ubuntu',
                float version = 22.04,

        __init__(self){
            self.id = generateID();
            self.cores = cores,
            self.specific_cores = []*cores,
            self.memory = memory,
            self.disk_gb = disk_gb,
            self.os = 'Ubuntu',
            self.version = 22.04,
        }  

        reserve(self){}

        activate(self){}

        deactivate(self){}

        release(self){}
    }
</details>

<details>
    <summary> Virtual Circuit Class </summary>

    class VC{
        int id,
        required int connections,
        required int bandwidth,
        required Object<Generic>[] children,
        
        __init__(self){
            self.id = generateID(),
            self.connections,
            self.bandwidth,
            self.children,
        }

        reserve(self){
            addToDatabase(self);
            for(child in self.children){
                child.reserve();
            }
        }

        activate(self){
            setStateInDatabase('active');
            for(child in self.children){
                child.activate();
            }
        }

        deactivate(self){
            setStateInDatabase('deactive');
            for(child in self.children){
                child.deactivate();
            }
        }

        release(){
            removeFromDatabase(self);
            for(child in self.children){
                child.release();
            }
        }
    }
</details>

<details>
    <summary> Composite Class </summary>
    
    class Composite{
        int id,
        required Object<Generic>[] children,

        reserve(self){
            addToDatabase(self);
            for(child in self.children){
                child.reserve();
            }
        }

        activate(self){
            setStateInDatabase('active');
            for(child in self.children){
                child.activate();
            }
        }

        deactivate(self){
            setStateInDatabase('deactive');
            for(child in self.children){
                child.deactivate();
            }
        }

        release(self){
            removeFromDatabase(self);
            for(child in self.children){
                child.release();
            }
        }
    }
    
</details>


<details>
    <summary> Server Class </summary>
    
    class Server{
        int id,
        required int available_cores,
                int[] available_specific_cores = [0*cores],
        required int memory,
        required int disk_gb,
        required Object<Generic>[] children,


        reserve(self){
            addToDatabase(self);
            for(child in self.children){
                child.reserve();
            }
        }

        activate(self){
            setStateInDatabase('active');
            for(child in self.children){
                child.activate();
            }
        }

        deactivate(self){
            setStateInDatabase('deactive');
            for(child in self.children){
                child.deactivate();
            }
        }

        release(self){
            removeFromDatabase(self);
            for(child in self.children){
                child.release();
            }
        }
    }
</details>

### Database Example without Encapsulation

| instance_id     | owner (uid) | object            | editable  | state  | last update (unix timestamp)|
|:--------------: |--------|------------------------|-----------|--------| ------------|
| hQCgymmGn1g=    |  colby |  Server{id: 1, children:[QyE3mtUwsrM=]}         |  false    | active | 1672952148  |
| QyE3mtUwsrM=    |  colby |  Composite{id: 1, children: [1z4mjTzXon4=]}      |  false    | active | 1672952148  |
| YqgMh+K+bE4=    |  colby |  VM{id: 1}             |  false    | active | 1672952148  |
| ZaLfxYqXj7o=    |  colby |  VM{id: 2}             |  false    | active | 1672952148  |
| 1z4mjTzXon4=    |  colby |  VC{id: 1, children: [YqgMh+K+bE4=,ZaLfxYqXj7o=]}             |  false    | active | 1672952148  |


### Database Example with Encapsulation

| instance_id     | owner (uid) | object     | editable  | state  | last update (unix timestamp)|
|:--------------: |--------|-------------    |-----------|--------| ------------|
| YqgMh+K+bE4=    |  colby |  Server{id:1, children: [Composite{id:1}]}  |  false    | active | 1672952148  |
| hQCgymmGn1g=    |  colby |  Composite{id:1, children: [VM{id:1}, VM{id:2}, VC{id:1}]}  |  false    | active | 1672952148  |
