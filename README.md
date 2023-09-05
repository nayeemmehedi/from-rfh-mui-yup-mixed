# from-rfh-mui-yup-mixed
      
      import React from 'react';
      import { useForm, Controller } from 'react-hook-form';
      import { TextField, Button } from '@mui/material';
      import { Alert, Space, Input } from 'antd';
      import { yupResolver } from '@hookform/resolvers/yup';
      import * as yup from 'yup';
      
      const schema = yup.object().shape({
        name: yup.string().required('Name is required'),
        email: yup.string().email('Invalid email').required('Email is required'),
        password: yup.string().min(6, 'Password must be at least 6 characters').required('Password is required'),
      });
      
      const LoginCmp= () => {
        const { control, handleSubmit, formState: { errors } } = useForm({
          resolver: yupResolver(schema),
        });
      
        const onSubmit = (data) => {
          console.log(data);
        };
      
        return (
          <form onSubmit={handleSubmit(onSubmit)}>
            <Controller
              name="name"
              control={control}
              defaultValue=""
              render={({ field }) => (
                <TextField
                  {...field}
                  label="Name"
                  variant="outlined"
                  fullWidth
                  error={!!errors.name}
                  helperText={errors.name?.message}
                />
              )}
            />
      
            <Controller
              name="email"
              control={control}
              defaultValue=""
              render={({ field }) => (
                <TextField
                  {...field}
                  label="Email"
                  variant="outlined"
                  fullWidth
                  error={!!errors.email}
                  helperText={errors.email?.message}
                />
              )}
            />
      
            <Controller
              name="password"
              control={control}
              defaultValue=""
              render={({ field }) => (
                <Input.Password
                  {...field}
                  placeholder="Password (Ant Design)"
                  style={{ width: '100%' }}
                  error={!!errors.password}
                />
              )}
            />
      
            <Space>
              <Button variant="contained" type="submit">
                Submit (MUI)
              </Button>
              <Button variant="contained" type="button">
                Reset (MUI)
              </Button>
            </Space>
      
            <Alert
              message="Note: Ant Design and Material-UI components are used in this form."
              type="info"
              style={{ marginTop: '16px' }}
            />
          </form>
        );
      };
      
      export default LoginCmp;
