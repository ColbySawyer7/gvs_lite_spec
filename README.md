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

