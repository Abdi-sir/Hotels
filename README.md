# Hotels Project
how we set up eslint
  - installing eslint 
    npm install -save-dev vite-plugin-eslint eslint-config-react-app eslint
  - create .eslintrc.json file
     - {
         "extends" : "react-app"
          }
  - add eslint to the vite.config.js file
        import { defineConfig } from 'vite'
        import react from '@vitejs/plugin-react'
        import eslint from 'vite-plugin-eslint'
        
        // https://vitejs.dev/config/
        export default defineConfig({
          plugins: [react(),eslint],
        })

# here is the note for the project
here is basic steps of doing react project here
 - first finding the problem statement of the project
 - basic tools that used for profectianal react project 
     - react router for single page application
     - react styled component 
     - react query
     - context api for state management
     - react hook form 
     - react icon
     - react rechart
     - raect hot toast
     - date-fns
     - supabase
 - starting the project
    - starting install vite
    - installing and enableing esLint and adding to vite configaration
    - set the folder 
      - data
      - features
      - hooks
      - pages
      - servises
      - styles
      - ui
      - utils
    - then installing the styled component to handdle symply use styled component extention
      using global styled component 
    - adding google font link
    - setting up pages and reoutes
    - installing react router dom
    - ??check data loading feature in the using react router
      after finishing this big project need to revise the profectional project in this project
     - using <browserroute><routes><route path='' element={<pagename/>}/ </routes></browserroute>

     - selecting the default homepage and error pagenot found
        - index route 
          <route index element={<pagename/>}/>
          or
                    <route index element={<Navigate replace to='pathname'/>}/>
        - * 
          <route path="*" element={<pagenotfound/>}/>
    - then adding the global style
    - building the application layout in the ui folder
       - then adding layout route to the app like this
        <route element={<applayout/>}
         place other route iside it as child exept login and page not found
        </route> , it do
        - then inside the applayout conponent call the <outlate/> below the design
        means   <Header/>
                <Sidebar/>by aside tag  
                <main>
                <outlate/>
                </main>
                using grid and felx css grid-row:1/-1;
        - build main navigation in the Sidebar
          <nav>
           <ul>
             <li><Link href='/page name'>home</link></li>
           </ul>
          </nav>
          use navlik instead of link
          <navlik to="/pagename"></navlik>
          to styled it const link = styled(navlink)`` thed adding svg icon from react icon install it then use
          - then configering supabase 
          -creating database and tables , then adding row level security and adding new policy
          - connecting supabase to react app
          how - install supabase pachage using npm
              - creating config file in the service folder supabase.js
              -then after we can build the api inside it
               export async function getSomething(){

               }
               - then after creating supabase storage bucket for storing images and 
      - 
    - now we have to try to talk about react qyery
        -setting up react querry
         - installation ant tanstack
         - set up into our application like context api
           - create aplace where the data is stroed or catch then connect to our application
          by using queryclient  
          how to set up this 
          const queryClient = new QueryClient({
            defaultOptions:{
              staleTime://this is how much is the time tbe refetched
            }
          })
        then after add to app <queryClientProvide client={queryClient}></queryClientProvide>
        //we can have react query dave tool by installing and adding the app as the first child of <reactQuerydavetool initialpoint={false} />
        so we have to store the data in one place then we can access to every where like what we have did in redux

        - lets start fetching data 
           - the first function is useQuery() 
           const data = useQuery({
            it needs queryKey: [''] that identify the data
            then queryFunction : fetch(...url) or using user predefind api function like getSomething function isnside 
           }) we have the data and other states so we can access any thing about the data lets pick some of them 
           isLoading or status lets accept 
           const {isLoading,data,error} = useQuery({...the hole thing})
           if(loading) return <spinner/>
           otherwise we can heve the data then return to ower screen 
           return (
            {data.map((passeddata)=>(<displaytagelemet data={data} key={data.id}/>))}
           )
           <displaytagelemet/>this coponent accepting the data thed distrcute it what weant and display   
           //check the formatcurrency  by using date-fns pachage install and useit
           the main purpose and basic cocept of react query is no need of the system feting the data again becouse it keep it as a catch

           
        - how to mutate ower remote state
         that means like deleting the data 
         first set up the api function for deletion  passing the id of the data then delete it
         how?
          using useMutation fucntion let distructure it
           const {isLoading,mutate} = useMutation({
            mutationFn:pass the id if the deleted function to the api delete fucntion (id)=>deletedata(id) or the deletefunction deletedate,
            and validate with onsuccess
            onsuccess:()={
              alert() //replace this by using toasts display for any notification change something 

              //in this we need to pass the invalidate to the app so use the  queryclient here
              queryClient.invalidatequeryclient({
                //pass the queryKey
                queryKey:[''] the sameto the feting key
                then we use onerror
                onError:(err)=>alert(err.message)
              })
            }
           })
           then after handele the delete buttonns like <button noclick={()=>mutate(dataid) disabled={isLoading}}>delete</button>
       -how to use toast 
         -install it first react-hot-toast
         - setup in theapp
           add <Toaster position .... other params />
           - then after we can use it anywhere in the application 
           onError:(err)=>toast.error(err.message) like this on success and on error 
           onsuccess: toast.success....

           //here is an other library react hook form to do with form simply no need of complex javascript equation to handle just simple line code lets use it

         fucntion creatinguserform(){
          //here we use the usefprm hook
          const {register,handlesubmit}=useForm(); //simply it can give as lots of function automaticaly like onchane onblure typw ...etc by register object then after we input and pass the handlesubmit to the form and call owe own function 
          fucntion onsubmithandelr(data){
               using the data for what you want
          }
        return
        <form onsubmit={handlesubmit(onsubmithandelr)}>
             <input type= id='name' {...register('name)}>name </input>
        </form>
         }
         we can have the data simply no use of other state 
         simply define the function to insert don the api then pass the dota to the api when submit 
         to create or delete the data we need to mutuate the data so in order to insert or create the data we need useMutation fucntion to connect the apt and the data
         so 
          fuction createdata(){
            const {register,handlesubmit,reset} = useForm()
            const {mutate,isLoading}=useMutation({
              mutationFn:createdata from the api
              onsuccess:()=>{
                toast.success(........),
                reset()
              }
              queryClient.invalidatequeryclient....
              onError....
            })
             fucntion onsubmit(data){
              mutate(data)
             }
          }
        - the other use of useform hook is to handele the error simply shown below
        //appliying to the out line select the spesfic part and add property css like overfolow scrol and so
        lets go to form validation syply from register object of useform function 
        <input type.. id.. {...register('idname',{required:'this is required'})}...add more max min validate with getvalues...
        pass the fucntion to the form like this
        <form onsubmit={handlesubmit(onsubmithandelr,onerror)}>
        </form>
          onerror(){
            //here we can use or not this function
          }
        but howt ro display this error to the user ==> byusing formstate function
        const {register,handlesubmit,reset,getvalues,formstate} = useform()
        const {errros} = formstate()
        so new we can pass it to any line of code sumply
        <input></input>   
        {errros?.name?.message&&<error>{errros.name.message}</error>} make it one component and re use it 
       - here is the best part how to upload the image to supabsase 
          <img id="image" {...register("image"),{required....}}/>

          then we need to pass to onsubmit function 
          fucntion onsubmit(data){
            mutate({..data,image:data.image.at(0)})
          }

          //creating the upload function inside the api  - create data then upload the data
          const imageName = `${Math.radom()}-${newdata.image.name}`.replaceAll("/","");
          const imagePath = `${grapthesupabaseurl}/..../../${imageName}`;
          then creating data
          const {data,err} =await supabase.from('c').insert([{...newdata,image:imagePath}])

          //then lets upload the image from the api doc
          const {error}=await supabase.storage.from("bucketname).upload(imagename,newdata.image)

          //delet the data if an error in uploading the image
          if(error){
            await supabase.from('').delete().eq("id",data.id)
            throw new error ()
          }
           return data
        - editing the data
            - first adding edit button then pass the data to edit form may the same to create data , here the question is how to pass the data to the form and display on edit from so 
            by using useForm
            function createdata({datatoedit={}}){
             const {id:editid,..editvalue} = datatoedit;
             const isEditSession = boolean(editid);

             cosnt {register,handlesubmit,reset,getvalues,formstate}=useForm(
              {
                defaultValues:isEditSession?editvalue:{}
              }
             )   



            } 
            <button >{make it for edit and creaete}</button>
            then how to handel the file uploading section of the editing 
            make the <img {...register('image',{
              required:isEditSession?false:"this field is required"
            })}

            then after let back to api to create the edit function so 
            use the create data function and modify some of it
            replace with
            function async createEditdata(newData,id){ 

            //in this edition section we need to specify the path of the image 
            so check it
            const hasImagePath = newdata.image?.startwith(supabaseUrl)
            modify the image pathe like this
            const imagePath =  hasImagePath?newdata.image:`${supabaseUrl}/v1...../${imageName}



              const imageName....
              imagePath...
              let query = supabase.form("tablename")
              if(!id)
             query =  
             query.insert([{....newdata,image:imagePath}])
              if(id) query = 
              //get the code in supabase api
              query.update({....newdata,image:imagePath}).eq("id",id)
              //need row level security
             cosnt {data,error} = await querry.select().single();
             if(error)....
      

             } 

             after all we now use that function in the mutation
             that is the same to other 
             in the form section 
             const queryClient = useQueryClinet();
             const {mutate:editData,isLoading:isEditing}=useMutation({
              mutationFn:({newdata,id})=>createEditData(newdata,id),onsuccess....
             })

             then we can both check

             const isworking = isCreating||isEditing //then repalce all with is working 
             fucntion onsubmit(data){
              //we need to check if it is string path of image 
             cosnt image = typeof data.image === 'string'?data.image:data.image[0] 
             if (isEditSession)
             editData({newdata:{...data,image},id:editid})
             else createdata({...data})
               }


      - now we are going to make custom hooks 
     lets do the delete part
     useDelet.js
     fucntion useDelete()
    {

      return{isDeleting,deletData}
    }
       on the button
       <button onclick={()=>delete(dataId)}></button>

       ..........
       duplictae a data
       <button>Duplicate</button> use the create data user defaind hook for duplication
       const {isCreating,createdata}=useCreatedata()
       fucntion handleduplicate(){
        createdata({name:`copy of ${name}`,maxcapa....})
       } 
       <button onclick={handleduplicate} disabled={isCreating}>Duplicate</button>
       here we need to fix on api that handel create data for image path if the path is 
       if(hasImagePath) return data; place it befor upload
     
     now we are going to build the applictation settings
     in the supabase in the authentication create policy for settings
     in the api of seeting we use the select("*").single() becouse of we select single instead of array of objects 

     // we have build the update and feting actually geting the data for setting api so and also we have useStting hook for ffetvhing with useQuery function
     for the update api
     look we need only one row of setting for update so
     export async function updateSetting(newSetting){
      const {data,err} =await supabase.from("setting").update(newStting).eq("id",1).single()
     }
      we can use the useCreate hook we create before change for setting 
     after all when we implement the setting when we leave the box is unBlur attribute
     <input type name onBlur={(e)=>handeleUpdate(e,"minlength")}/>

     function handeleUpdate(e){
       const {value} = e.target
       if(!value) return;
       updateSetting({[filed]:value})
     }
     use for all other field 


///////////////////////
advanced react pattern 
code reusability is 
 ui reusability and stateful logic (hook)
  

  