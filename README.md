package test;

import java.lang.reflect.Field;
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

public class DoInvoke {

	public static void main(String[] args) {
		
		
		// TODO Auto-generated method stub
		TestBean testBean = new TestBean();
		testBean.setName1("name11");
		testBean.setName2("name22");
		testBean.setTable1("table11");
		testBean.setTable2("table22");
		Map<String,String> nametransfer = new HashMap<String,String> ();
		nametransfer.put("name11", "qi");
		nametransfer.put("name22", "fu");
		Map<String,String> tabletransfer = new HashMap<String,String> ();
		tabletransfer.put("table11", "ming");
		tabletransfer.put("table22", "yao");
		invoke(testBean , nametransfer, tabletransfer);

	}
	
	public static TestBean invoke (TestBean testBean,Map<String,String> nametransfer,Map<String,String> tabletransfer) {
		
		Arrays.asList(testBean.getClass().getDeclaredFields()).stream().forEach(f->{
			f.setAccessible(true);

			try {
				if(f.getName().startsWith("name")) {
					String value = f.get(testBean).toString();
					f.set(testBean, nametransfer.get(value));
				}else {
					String value = f.get(testBean).toString();
					f.set(testBean, tabletransfer.get(value));
				}
			} catch (IllegalArgumentException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			} catch (IllegalAccessException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			
		});
		Arrays.asList(testBean.getClass().getDeclaredFields()).parallelStream().filter
		(f->f.getName().startsWith("name")).forEach
		(f->{
			f.setAccessible(true);

			try {
				String value = f.get(testBean).toString();
				f.set(testBean, nametransfer.get(value));
			} catch (IllegalArgumentException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			} catch (IllegalAccessException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			
		});
		Arrays.asList(testBean.getClass().getDeclaredFields()).parallelStream().filter
		(f->f.getName().startsWith("table")).forEach
		(f->{
			f.setAccessible(true);

			try {
				String value = f.get(testBean).toString();
				f.set(testBean, tabletransfer.get(value));
			} catch (IllegalArgumentException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			} catch (IllegalAccessException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			
		});
		Arrays.asList(testBean.getClass().getDeclaredFields()).parallelStream().map(a->a.getName()).filter(name->name.startsWith("table")).forEach(System.out::println);
		System.out.println(testBean.getName1()+testBean.getTable1());
		System.out.println(testBean.getName2()+testBean.getTable2());
		return null;
	}

}
