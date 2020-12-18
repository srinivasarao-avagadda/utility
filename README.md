private static void getJSONByPath(String path,JSONObject obj, List<Object> list) throws JSONException  
    {
        
        if(path != null)
        {
            if(!path.contains("."))
            {
                if(obj.has(path) && obj.get(path) != null)
                {
                    Object retObj = JSONUtils.safeGetJSONObject(path, obj);
                    if(retObj != null)
                    {
                        if(retObj instanceof JSONArray)
                        {
                        	list.add(new JSONArray(retObj.toString()));
                        }
                        else if(retObj instanceof JSONObject)
                        {
                            list.add(new JSONObject(retObj.toString()));
                        }
                        else
                        {
                            list.add(new String(retObj.toString()));
                        } 
                    }
                    
                }
            }
            else
            {
                String node = path.split("\\.")[0];
                if(obj.has(node) && !obj.isNull(node))
                {
                    Object newNode = obj.get(node);
                    if(newNode instanceof JSONObject)
                    {
                        JSONObject jObj = (JSONObject) newNode;
                        getJSONByPath(path.substring(path.indexOf(".")+1), jObj,list);
                    }
                    else if(newNode instanceof JSONArray)
                    {
                        JSONArray jArr = (JSONArray)newNode;
                        for(int i=0;i<jArr.length();i++)
                        {
                            JSONObject jObj = jArr.getJSONObject(i);
                            getJSONByPath(path.substring(path.indexOf(".")+1), jObj,list);
                        }
                    }
                }
            }
        }
    }
