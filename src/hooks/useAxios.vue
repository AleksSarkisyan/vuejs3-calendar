<script lang="ts">

import axios from 'axios';

export default function useAxios() {
  const call = async ( { method, path, data } ) => {
    /** For demo only, must be in .env */
    let url = 'http://localhost:3000/' + path;

    try {
      const response = await axios({
        method,
        url,
        data
      });

      return response;
    } catch (error) {
      console.log('error --', error.response.data)

      throw error;
    }
  };

  const get = async (path: string, data?: object | null) => {
    return await call({ method: 'GET', path, data });
  };

  const post = async (path: string, data?: object | null) => {
    return await call({ method: 'POST', path, data });
  };

  return {
    get,
    post
  };
}

</script>
